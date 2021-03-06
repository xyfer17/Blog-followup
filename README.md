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

