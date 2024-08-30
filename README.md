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
 
 ## how to kill the port process
```
$ sudo kill -9 $(sudo lsof -t -i:<port>)
```

# How to Dockerize An application

## 1. Dockerize the Application:

Create a file named Dockerfile in the same directory as server.js:

``` Dockerfile

#  Use an official Node.js runtime as a base image
FROM node:14

#  Set the working directory inside the container
WORKDIR /app

#  Copy package.json and package-lock.json to the container
COPY package*.json ./

#  Install application dependencies
RUN npm install

#  Copy the rest of the application code to the container
COPY . .

#  Expose the port specified in the PORT environment variable
EXPOSE ${PORT}

#  Start the application
CMD ["node", "server.js"]

``` 
## 2. Build the Docker Image:

Open a terminal in the directory containing server.js and Dockerfile and run:


```docker build -t <image_name> .```

## 3. Run the Docker Container:

You can run the Docker container, binding the container's port to the host machine's port using the -p flag. The port will be set according to the PORT environment variable you specify:



``` docker run -d -p <host_port>:<container_port> -e <ENV_VARIABLE>=<value> <image_name> ```


## To rebuild a running Docker container with changes in the codebase, you need to follow these steps:

1. **Stop the Running Container:**
   First, you need to stop the running container to free up its resources and ports. You can use the `docker stop` command followed by the container's ID or name:

   ```bash
   docker stop <container_id_or_name>
   ```

2. **Update the Codebase:**
   Make the necessary changes to your codebase.

3. **Rebuild the Docker Image:**
   After updating the codebase, you need to rebuild the Docker image. Navigate to the directory where your `Dockerfile` is located and run the `docker build` command:

   ```bash
   docker build -t <image_name> .
   ```

   Replace `<image_name>` with the desired name for your image.

4. **Run a New Container:**
   Once the new image is built, you can run a new container using the updated image. Be sure to map the ports and set any environment variables as needed:

   ```bash
   docker run -d -p <host_port>:<container_port> -e <ENV_VARIABLE>=<value> <image_name>
   ```

   Replace `<host_port>` and `<container_port>` with the appropriate port numbers, and `<ENV_VARIABLE>` and `<value>` with any environment variables your application requires.

By following these steps, you're effectively stopping the existing container, rebuilding the Docker image with the updated codebase, and then running a new container using the updated image.

Remember to tailor the commands and steps to your specific project structure and requirements.


## - Containerizing a React application inside a Docker container involves a series of steps. Here's a basic guide to get you started:

**1. Build the React Application:**

First, make sure you have a working React application that you want to containerize. If you don't have one yet, you can create a new React application using `create-react-app`:

```bash
npx create-react-app my-react-app
cd my-react-app
```

**2. Create a Dockerfile:**

In the root directory of your React application, create a file named `Dockerfile` with the following content:

```Dockerfile
# Use an official Node.js runtime as the base image
FROM node:14

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install application dependencies
RUN npm install

# Copy the rest of the application code to the container
COPY . .

# Build the React app
RUN npm run build

# Expose a port that the application will listen on
EXPOSE 3000

# Start the application
CMD ["npm", "start"]
```

**3. Build the Docker Image:**

Open a terminal in the directory containing your React application's `Dockerfile` and run:

```bash
docker build -t react-app-container .
```

**4. Run the Docker Container:**

After building the Docker image, you can run a container using the following command:

```bash
docker run -d -p 8080:3000 react-app-container
```

This will map port 8080 on your host to port 3000 in the Docker container. Adjust the port numbers as needed.

**5. Access the React Application:**

You can access your React application in a web browser by navigating to `http://localhost:8080` (or the port you specified) in your host machine.

Please note that this is a basic example. In a real-world scenario, you might need to configure environment variables, handle more advanced application setup, and consider best practices for Docker images and containers.

Additionally, if you're planning to deploy the Dockerized React application, you'll need to consider how to deploy it to a cloud platform, set up a reverse proxy, configure CI/CD pipelines, and more, depending on your project's requirements.

**6. To Remove UNTAG docker images**
```
docker system prune -f
```

## How create a new git repo

```
echo "# monolithic_structure" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/xyfer17/monolithic_structure.git
git push -u origin main
```
## How to execute the postgres

```
docker exec -it <your-postgres-container-name> psql -U postgres
```

## Steps for branching from main and switch to main
```
git switch main
git checkout -b <branch-name>
```

## How to setup django 

```
$ django-admin startproject mysite
```

### Let’s look at what startproject created:
```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```
The development server¶
Let’s verify your Django project works. Change into the outer mysite directory, if you haven’t already, and run the following commands:

```
$ python manage.py runserver
```
To create your app, make sure you’re in the same directory as manage.py and type this command:

```
$ python manage.py startapp appName
```

That’ll create a directory polls, which is laid out like this:

```
appName/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```

for more ref: [tutorial 1](https://docs.djangoproject.com/en/5.0/intro/tutorial01/)

## How to Deploy Node App 

To deploy a Node.js app on an EC2 instance, you can follow these general steps:

### 1. **Set Up the EC2 Instance**
   - **Launch an EC2 Instance**: Use the AWS Management Console to launch an EC2 instance. Choose an appropriate Amazon Machine Image (AMI) like Ubuntu or Amazon Linux.
   - **Configure Security Group**: Open necessary ports, especially:
     - Port 22 for SSH access.
     - Port 80 for HTTP or Port 443 for HTTPS if you plan to serve your Node.js app over the web.
   - **Connect to the EC2 Instance**: Use SSH to connect to your EC2 instance.

### 2. **Install Node.js**
   - **Update Package Index**:
     ```bash
     sudo apt-get update
     ```
   - **Install Node.js**: You can install Node.js using the NodeSource repository.
     ```bash
     curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
     sudo apt-get install -y nodejs
     ```
   - **Verify Installation**:
     ```bash
     node -v
     npm -v
     ```

### 3. **Transfer Your Node.js App**
   - **Using Git**: Clone your repository to the EC2 instance.
     ```bash
     git clone https://github.com/your-repository.git
     ```
   - **Using SCP/FTP**: Alternatively, you can use SCP or FTP to upload your app to the EC2 instance.

### 4. **Install Dependencies**
   - Navigate to your app directory and install the necessary dependencies:
     ```bash
     cd your-app-directory
     npm install
     ```

### 5. **Set Up Environment Variables**
   - You can set up environment variables using a `.env` file or directly in the terminal.

### 6. **Run the Application**
   - Start your Node.js application:
     ```bash
     node app.js
     ```
   - For production environments, use a process manager like **PM2** to manage your app:
     ```bash
     npm install -g pm2
     pm2 start app.js
     pm2 startup
     pm2 save
     ```

### 7. **Set Up Reverse Proxy (Optional)**
   - If you want your app to run on port 80 (HTTP) or 443 (HTTPS), set up a reverse proxy using **Nginx**:
     - Install Nginx:
       ```bash
       sudo apt-get install nginx
       ```
     - Configure Nginx:
       ```bash
       sudo nano /etc/nginx/sites-available/default
       ```
       Update the file with something like this:
       ```nginx
       server {
           listen 80;
           server_name your-domain.com;

           location / {
               proxy_pass http://localhost:3000;
               proxy_http_version 1.1;
               proxy_set_header Upgrade $http_upgrade;
               proxy_set_header Connection 'upgrade';
               proxy_set_header Host $host;
               proxy_cache_bypass $http_upgrade;
           }
       }
       ```
     - **Restart Nginx**:
       ```bash
       sudo systemctl restart nginx
       ```

### 8. **Set Up a Domain Name (Optional)**
   - If you have a domain, you can set it up with Route 53 or another DNS provider to point to your EC2 instance's public IP.

### 9. **Automate Deployment (Optional)**
   - Consider using CI/CD tools like **GitHub Actions**, **Jenkins**, or **AWS CodeDeploy** to automate the deployment process.

By following these steps, your Node.js app should be successfully deployed and running on an EC2 instance.
