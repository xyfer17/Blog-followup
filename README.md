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

