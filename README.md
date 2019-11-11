# OpenGL-CMake-Config

## A CMake configuration for Visual Studio cross platform development.
* Contains configuration for:
* SDL2 (cross platform contexting)
* Bullet3 (3D Physics engine)
* GLM (Math library commonly used alongside OpenGL)
* glew (OpenGL extension loading library)
* GameNetworkSockets (Basic networking library for games)

slightly based off of https://github.com/ArthurSonzogni/OpenGL_CMake_Skeleton

# Building

Just a heads up: This is not an easy build process, but I added some scripts to make this process go as smooth as possible.
Some of the CMake scripts and library linking could definitely be considered 'hacky' but I'm justifying it by saying it works, and it's mainly built for my own dev environment.

If you end up using this for your own projects, hope you enjoy!

### Windows 10 install for Visual Studio Cross Platform
* Git clone --recursive
* open root dir in Visual Studio
* Supply CMake settings
* install https://slproweb.com/products/Win32OpenSSL.html - both 86 and 64. These are used to build Google protobuf
* navigate to /lib/protobuf_build
* run populate_all.bat and supply your version of VsDevCmd.bat as an arg. 

ex:
```populate_all.bat "C:\Program Files (x86)\Microsoft Visual Studio\2019\Preview\Common7\Tools\VsDevCmd.bat"```

Protobuf should then be installed in C:\sdk\protobuf
This WILL take awhile. 

* navigate to /lib/gamenetworksockets_build
* run populate_all.bat and supply your version of VsDevCmd.bat as an arg. 

ex: 
```populate_all.bat "C:\Program Files (x86)\Microsoft Visual Studio\2019\Preview\Common7\Tools\VsDevCmd.bat"```

GameNetworkSockets should then be installed in /lib/gamenetworksockets_build This shouldn't take as long as it took protobuf to build.

* Create a vm for linux. I used Ubuntu 16.04. This could also be a real machine you can ssh into.
* Configure ssh login for linux machine (not going to go into this, plenty of tutorials)
* Add machine ssh credentials to cmakesettings

#### Configure linux machine for development
Install SDL2:
``` 
apt-get sdl2 
```
Install libssl:
```
apt install libssl-dev
```
Now if you're unlucky like me, you might need to update libssl and apt-get wont do the job. This awesome tutorial will show you how to update libssl from it's source:
https://www.howtoforge.com/tutorial/how-to-install-openssl-from-source-on-linux/

Install protobuf:
```
apt install libprotobuf-dev protobuf-compiler
```
Install ninja
apt install build-ninja

Install gamenetworkingsockets:
```
git clone 
cd gamenetworkingsockets
mkdir build
cd build
cmake -G Ninja ..
ninja
```

Optional but I move the output files into lib where sdl is
```
cd src
mv libGameNetworkingSockets_s.a /usr/lib/x86_64-linux-gnu
mv libGameNetworkingSockets.so /usr/lib/x86_64-linux-gnu
```

## Debuging
* Double check CMakeSettings like SDL2_DIR and GNS_LIB_DIR, they should both point to their library directories.
* The populate_all scripts need to be supplied with VsDevCmd.bat. The path for VsDevCmd.bat differs on each version of visual studio.
* Lots of trial and error. Building this first try with no errors seems unlikely.
