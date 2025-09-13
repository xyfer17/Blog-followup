# Group Rules IndexedDB Implementation - Updated

## Overview

This implementation provides a comprehensive solution for tracking Group Rules changes using IndexedDB with unique ruleName-based tracking. The unique `ruleName` is generated in the base-layout component when new rows are created, ensuring proper change tracking.

## Key Features

### 1. Unique Rule Name Generation
- **Location**: Generated in `base-layout.component.ts` when new rows are created
- **Format**: `Rule_${randomString}_${timestamp}`
- **Generated in**:
  - `AddMoreValues()` - when adding new rows to existing expressions
  - `createFormGroup()` - when creating new form groups
  - `updateExpressionValue()` - when creating new rows during value updates
  - `updateHeaderValue()` - when creating new rows during header updates
  - `updateValueByPropName()` - when creating new rows during property updates

### 2. Change Detection Logic
- **Create**: Row without `ruleId` → stored as "create" type
- **Update**: Row with `ruleId` → stored as "update" type  
- **Delete**: Row with `ruleId` being deleted → stored as "delete" type
- Multiple changes to the same row are consolidated under the same `ruleName`

**Change Tracking Points:**
- `updateValueByPropName()` - when row properties change
- `updateExpressionValue()` - when condition values change
- `updateExpressionRootValue()` - when expression root-level fields (value, assignTo, mapWhen) are updated
- `deleteRowValue()` - when rows are deleted
- `updateExpressionHeader()` - when attribute headers are updated
- `updateOperator()` - when operators are updated
- `deleteExpressionValueHandler()` - when attributes are deleted
- `addNewExpressionValue()` - when new attributes are added
- `deleteRuleHandler()` - when entire rules are deleted
- `switchExpressionValueHandler()` - when switching between expression and condition builder

**Data Included in Changes:**
- `ruleName` - unique identifier for the row
- `isExpression` - whether the rule is an expression or condition builder
- `priority` - priority of the expression
- `expressionIndex` - index of the expression in the form
- `rowIndex` - index of the row within the expression

**Special Handling:**
- **Rule Deletion**: `deleteRuleHandler()` emits delete changes for all rows with `ruleId` in the deleted expression
- **Expression Switching**: `switchExpressionValueHandler()` emits delete changes for existing rows and create changes for the new default row
- **Backward Compatibility**: Legacy `deleteRule.emit()` events are still emitted alongside new IndexedDB tracking
- **Groups Only**: All `emitRowDataChange()` calls are wrapped with `if (this.isGroups)` condition - IndexedDB tracking only occurs when `isGroups` is true

### 3. IndexedDB Storage
- Uses `ruleName` as the primary key for efficient lookups and updates
- Changes to the same row (same `ruleName`) are automatically updated rather than duplicated
- Group rules component receives the `ruleName` from base-layout component

### 4. Validation Flow
- **Pre-Processing Validation**: All changes are validated before processing
- **Condition Builder Rules**: Validates `assignTo` and `conditions` array with values
- **Expression Rules**: Validates `value` and `assignTo` fields
- **Expression Generation**: Only generates expressions if validation passes
- **Skip Invalid Rules**: Invalid rules are skipped with warning logs

### 5. Dynamic Data Updates (No Component Recreation)
- **Target Groups**: `targetGroupsList` changes are automatically detected via setter
- **Source Attributes**: `sourceListArrayChange$` updates attributes without recreating component
- **Auto Suggestions**: `autoSuggestionListChange$` updates suggestions without recreating component
- **In-Place Updates**: All data changes update the injected component directly
- **Performance**: Avoids expensive component destruction and recreation

### 6. Automatic Cleanup
- **Component Unmount**: IndexedDB is cleared when component is destroyed
- **Page Refresh**: IndexedDB is cleared on `beforeunload` event
- **Navigation Away**: IndexedDB is cleared when page becomes hidden

## Implementation Flow

1. **Row Creation**: Base-layout component creates new row with unique `ruleName`
2. **Change Detection**: Base-layout component detects changes and emits event with `ruleName`, `isExpression`, and `priority`
3. **Storage**: Group rules component stores change in IndexedDB using provided `ruleName`
4. **UI Update**: Pending changes summary is displayed
5. **Save Trigger**: User clicks save or external trigger is fired
6. **Validation**: Each change is validated before processing
7. **Expression Generation**: Only valid rules have expressions generated
8. **API Processing**: Valid changes are processed by type (create/update/delete)
9. **Cleanup**: Successfully processed changes are removed from IndexedDB

## Code Structure

### Base Layout Component (`base-layout.component.ts`)
- Generates unique `ruleName` for all new rows
- Emits change events with `ruleName` included
- Handles all row creation scenarios

### Group Rules Component (`group-rules.component.ts`)
- Receives change events with `ruleName` from base-layout
- Stores changes in IndexedDB using provided `ruleName`
- Processes changes during save operations
- Handles cleanup on component unmount

### IndexedDB Service (`group-rules-indexdb.service.ts`)
- Uses `ruleName` as primary key
- Provides upsert functionality for same-row changes
- Manages change storage and retrieval

## Benefits

1. **Consistent Rule Names**: All rows get unique names at creation time
2. **Efficient Updates**: Same row changes are consolidated under unique `ruleName`
3. **Proper Separation**: Base-layout handles row creation, group-rules handles storage
4. **Automatic Cleanup**: No stale data left behind
5. **Error Recovery**: Failed changes can be retried

## Usage

The implementation works automatically:
- New rows get unique `ruleName` when created
- Changes are tracked and stored in IndexedDB
- Save operations process all pending changes
- Cleanup happens automatically on component unmount or page refresh
