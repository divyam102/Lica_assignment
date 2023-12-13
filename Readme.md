## LIP SYNC 

## Setting up Openface (Building it from scratch)

# Cloning the Openface repo 
git clone https://github.com/TadasBaltrusaitis/OpenFace.git

# Install script 
cd OpenFace <br />
sudo bash ./install.sh

# Dependency Installation 

# GCC Installation 
sudo apt-get update <br />
sudo apt-get install build-essential <br />
sudo apt-get install g++-8

# Cmake Installation 
sudo apt-get install cmake <br />

# OpenBLAS 
sudo apt-get install libopenblas-dev <br />

# OpenCV 4.1.0 Installation 
sudo apt-get install git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev <br />

sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libdc1394-22-dev <br />

wget https://github.com/opencv/opencv/archive/4.1.0.zip <br />

sudo unzip 4.1.0.zip <br />
cd opencv-4.1.0 <br />
mkdir build <br />
cd build <br />

sudo cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D BUILD_TIFF=ON -D WITH_TBB=ON .. <br />
sudo make -j2 <br />
sudo make install <br />

# Download and compile dlib
wget http://dlib.net/files/dlib-19.13.tar.bz2; <br />
tar xf dlib-19.13.tar.bz2; <br />
cd dlib-19.13; <br />
mkdir build; <br />
cd build; <br />
cmake ..; <br />
cmake --build . --config Release; <br />
sudo make install; <br />
sudo ldconfig; <br />
cd ../..; <br />


## OpenFace Installation 

cd OpenFace (if not in Openface directory) <br />

mkdir build <br />
cd build <br />

# Compile the code using (if using g++ version 8, change to clang or other version appropriately):
cmake -D CMAKE_CXX_COMPILER=g++-8 -D CMAKE_C_COMPILER=gcc-8 -D CMAKE_BUILD_TYPE=RELEASE .. <br />
make <br />

# Test it with
./bin/FaceLandmarkVidMulti -f ../samples/multi_face.avi <br />

After building Openface from scratch move it to DINET folder , everything else is taken care of there  <br />
cd ../ <br />
rm -rf DINet/OpenFace (deleting the already present OpenFace inside DINet) <br />
mv OpenFace/ DINet/ <br />
cd DINet <br />

# Create a conda environment 
conda create -n lipsync python=3.9.18 <br />
conda activate lipsync <br />
cat requirements.txt | xargs -n 1 pip install <br />
(All the dependencies would be installed inside the activated environment) <br />

# To run the api i.e. run.py 

change line 287 (to add arguments for video path, audio path, gfpgan) <br />

```
obj.infer("/home/divyam/divyam/DINet/Drive.mp4", "/home/divyam/divyam/DINet/asserts/examples/driving_audio_1.wav", False)
```
arguments - <br />
"/home/divyam/divyam/DINet/Drive.mp4" - video path <br />
"/home/divyam/divyam/DINet/asserts/examples/driving_audio_1.wav" - audio path <br />
bool - True - would enable gfpgan <br />
    - False - would disable gfpgan <br />

python run.py <br />

# To run the gradio demo i.e. app.py <br />

change the example path accordingly <br />
line 42, 43, 44 <br />
```
["yourdirectorypath/DINet/asserts/examples/test1.mp4","yourdirectorypath/DINet/asserts/examples/driving_audio_1.wav"],
["yourdirectorypath/DINet/asserts/examples/test2.mp4","yourdirectorypath/DINet/asserts/examples/driving_audio_2.wav"], 
["yourdirectorypath/DINet/Drive.mp4","yourdirectorypath/DINet/asserts/examples/driving_audio_1.wav"], 
```
pip install gradio <br />
python app.py<br />