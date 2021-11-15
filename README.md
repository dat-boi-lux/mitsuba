# mitsuba-0.6.0-modern-linux
This is a fork of https://github.com/mitsuba-renderer/mitsuba with specific changes and instructions on how to compile for a more modern build of Linux/Ubuntu.
# Introduction:
Mitsuba 0.6.0 is a relatively old software. Many of the build instructions associated with the original https://github.com/mitsuba-renderer/mitsuba repository no longer work due to their age. This fork aims to allow Mitsuba to build on newer versions of Linux.\
\
These steps have been confirmed to work on **Linux Mint 20.2** (which is built on top of **Ubuntu 20.04**, so it should essentially be the same). Thank you to Jason Brenneman @ www.rrubberr.com for all the invaluable support.
# Build Instructions - Ubuntu:
First of all: Mitsuba 0.6.0 relies on **qt5** and its libraries in order to build the GUI. If you do not not care about the GUI, this step is not entirely necessary, although it is recommended to build the GUI for efficacy's sake. Install **qt5** and its libraries by typing these instructions into a terminal: \
\
```sudo apt install qt5-default``` \
```sudo apt install qtdeclarative5-dev``` \
```sudo apt install libqt5opengl5-dev libqt5xmlpatterns5-dev```\
\
Please note that if other versions of *qt* are installed  (such as *qt4*) there may be conflicts when building. You can remove *qt4* (or any other version of qt by typing this command into the terminal: WARNING: Only do this if you are aware of the repurcussions, other programs may rely on other versions of *qt*.\
\
```sudo apt purge qt4*``` ***Note***: replace the '4' with whatever qt version you wish to remove*\
\
Next install all the required dependencies by typing these instructions into a terminal: \
\
```sudo apt install build-essential scons git libpng12-dev libjpeg-dev libilmbase-dev libxerces-c-dev libboost-all-dev libopenexr-dev libglewmx-dev libxxf86vm-dev libeigen3-dev libfftw3-dev```\
\
You may already have some of these on your system so ignore any warnings saying that some things were not installed.\
\
Next enable and install **Collada** support by typing this into your terminal:\
\
```sudo apt install libcollada-dom-dev```\
\
Next ensure you have **Python 2.x** installed on your system. If you are using a newer version of Linux, you most likely have **Python 3.x** already installed and set as the default version of Python. The SCONS build system Mitsuba 0.6.0 uses; is not compatible with **Python 3.x** and will give you errors if used.\
\
Install **Python 2.x** by first adding this repository, then installing **Python 2.7**: (Type these instructions into your terminal). ***Note:*** **Python 2.7** is preferred as it is the newest **Python 2.x** version.\
\
```sudo add-apt-repository ppa:deadsnakes/ppa```\
```sudo apt update```\
```sudo apt install python2.7```\
\
This should do it for the dependencies. Now onto downloading **this repository** and building Mitsuba.\
\
Clone this repository onto your system. This is achieved by typing this command into your terminal:\
\
```sudo git clone https://github.com/dat-boi-lux/mitsuba-0.6.0-modern-linux.git```\
\
Now that you have cloned the repository onto your computer: navigate to where it has downloaded. On Ubuntu, this should be within your *Home* folder.\
\
Open a terminal within this folder. and then type this command into the terminal window you just opened:\
\
```QT_SELECT=qt5 python2 `which scons` -j32```\
\
An explanation for the command above: First we select the version of **qt** that we want to use (*`QT_SELECT=qt5`*). We try to be as specific as humanly possible so as not to confuse the build system. Then we select what version of **Python** we want to use (*`python2`*). This is to ensure that the build systems uses **Python 2.x** that we installed earlier. Next we tell the build system to find the "**SConstruct**" build file (*`which scons`*). Then we specify how many **CPU cores** we want to allocate to the build process (*`-j32`*). I have opted to use all **32** cores of my CPU, but if your CPU has less/more cores, you can specify this. Not specifying will result in SCONS defaulting to the use of only one core (this is **extremely slow**).\
\
You should now have successfully compiled and built Mitsuba 0.6.0. The binaries can be located in the "dist" directory that is created after a successful compile.
