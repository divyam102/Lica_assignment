## LIP SYNC 

## Setting up Openface 

# Cloning the Openface repo 
git clone https://github.com/TadasBaltrusaitis/OpenFace.git

# Install script 
cd OpenFace 
sudo bash ./install.sh

# Dependency Installation 

# GCC Installation 
sudo apt-get update
sudo apt-get install build-essential
sudo apt-get install g++-8

# Cmake Installation 
sudo apt-get install cmake

# OpenBLAS
sudo apt-get install libopenblas-dev

# OpenCV 4.1.0 Installation 
sudo apt-get install git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev

sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libdc1394-22-dev

wget https://github.com/opencv/opencv/archive/4.1.0.zip

sudo unzip 4.1.0.zip
cd opencv-4.1.0
mkdir build
cd build

sudo cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D BUILD_TIFF=ON -D WITH_TBB=ON ..
sudo make -j2
sudo make install

# Download and compile dlib
wget http://dlib.net/files/dlib-19.13.tar.bz2;
tar xf dlib-19.13.tar.bz2;
cd dlib-19.13;
mkdir build;
cd build;
cmake ..;
cmake --build . --config Release;
sudo make install;
sudo ldconfig;
cd ../..;    


## OpenFace Installation 

cd OpenFace (if not in Openface directory) 

mkdir build
cd build

# Compile the code using (if using g++ version 8, change to clang or other version appropriately):
cmake -D CMAKE_CXX_COMPILER=g++-8 -D CMAKE_C_COMPILER=gcc-8 -D CMAKE_BUILD_TYPE=RELEASE ..
make

# Test it with
./bin/FaceLandmarkVidMulti -f ../samples/multi_face.avi

After building Openface from scratch move it to DINET folder , everything else is taken care of there 
cd DINet 

# Create a conda environment 
conda create -n lipsync python=3.9.18
conda activate lipsync 
cat requirements.txt | xargs -n 1 pip install
(All the dependencies would be installed)

# To run the api i.e. run.py (line 287)

```
obj.infer("/home/divyam/divyam/DINet/Drive.mp4", "/home/divyam/divyam/DINet/asserts/examples/driving_audio_1.wav", False)
```
arguments - 
"/home/divyam/divyam/DINet/Drive.mp4" - video path 
"/home/divyam/divyam/DINet/asserts/examples/driving_audio_1.wav" - audio path 
bool - True - would enable gfpgan 
- False - would disable gfpgan 

python run.py

# To run the gradio demo i.e. app.py (line 287)

pip install gradio 
python app.py