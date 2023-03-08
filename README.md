# Blog

## How to install opencv from src


**install some dependencies**
```
sudo apt install build-essential cmake git pkg-config libgtk-3-dev \
    libavcodec-dev libavformat-dev libswscale-dev libv4l-dev \
    libxvidcore-dev libx264-dev libjpeg-dev libpng-dev libtiff-dev \
    gfortran openexr libatlas-base-dev python3-dev python3-numpy \
    libtbb2 libtbb-dev libdc1394-22-dev libopenexr-dev \
    libgstreamer-plugins-base1.0-dev libgstreamer1.0-dev

```

**clone the opencv repository**

```
git clone https://github.com/opencv/opencv.git
cd opencv
```
**Create a folder named `build`**

```
mkdir -p build && cd build
```

**Set up the OpenCV build with CMake:**
```
cmake ../
```
**Start Compilation**
```
make -j [no of core you want for the compilation.]
```

**Install**
```
sudo make install
```

**check the installation is completed perfectly**
```
python3 -c "import cv2; print(cv2.__version__)"
```

## git tutorial

**git credential save**

```
git config --global credential.helper store
```
## How to host react app on firebase

**step 1**
Install firebase in your working directory
```
npm install -g firebase-tools

```
**step 2**
Login the Firebase
```
firebase login
```

**step 3**
First, we will initialize a firebase project in our React app by running the following command in the console in our root directory.
```
firebase init
```
## How to make particular node version as  default using nvm
```
$ nvm alias default 16.14.2
$ nvm use

$ node -v
```

## How to set up Eslintrc Configuration

* step 1:
```
$ npm init @eslint/config
```
* step 2 : 
 [Click Here](https://levelup.gitconnected.com/configure-eslint-and-prettier-for-your-react-project-like-a-pro-2022-10287986a1b6)
