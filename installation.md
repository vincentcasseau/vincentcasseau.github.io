---
layout: page
title: Installation
--- 

### OF-v1706
{: #OF-v1706 }

1. Download the source .tgz files for Ubuntu (30/06/2017: OpenFOAM v1706) for both [OpenFOAM](https://sourceforge.net/projects/openfoam/files/v1706/OpenFOAM-v1706.tgz) and the [ThirdParty](https://sourceforge.net/projects/openfoam/files/v1706/ThirdParty-v1706.tgz)  
2. Untar them  
3. Install the [system requirements](https://www.openfoam.com/documentation/system-requirements.php) 
```sh
sudo apt-get update
sudo apt-get install build-essential flex bison cmake zlib1g-dev libboost-system-dev libboost-thread-dev libopenmpi-dev openmpi-bin gnuplot libreadline-dev libncurses-dev libxt-dev
sudo apt-get install qt4-dev-tools libqt4-dev libqt4-opengl-dev freeglut3-dev libqtwebkit-dev
sudo apt-get install libscotch-dev libcgal-dev
```
4. Install OpenFOAM    
```sh
cd $WM_PROJECT_DIR
./Allwmake
```
5. Change working directory and clone the hyStrath Github repository  
```sh
cd $WM_PROJECT_USER_DIR
git clone https://github.com/vincentcasseau/hyStrath.git --branch master --single-branch && cd hyStrath/
```
6. Decide which module(s) you wish to install
```sh 
./install.sh 8 2>/dev/null
```
where _8_ is the number of processors to be used during the installation (it can be edited).
