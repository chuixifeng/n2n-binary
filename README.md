### n2n-binary
n2n build from source 

#### use ubuntu20 biuld windowns exe

##### setup1 ubuntu20 depends
```
apt-get install mingw-w64 apt-get install cmake apt-get install openssl apt-get install libssl-dev apt-get install build-essential git bison flex libxml2-dev libpcap-dev libtool libtool-bin rrdtool librrd-dev autoconf pkg-config automake autogen redis-server wget libsqlite3-dev libhiredis-dev libmaxminddb-dev libcurl4-openssl-dev libpango1.0-dev libcairo2-dev libnetfilter-queue-dev zlib1g-dev libssl-dev libcap-dev libnetfilter-conntrack-dev libreadline-dev libjson-c-dev libldap2-dev rename libsnmp-dev
```
##### setup2 openssl dev env
```
wget https://www.openssl.org/source/openssl-1.1.1f.tar.gz 
tar -xvzf openssl-1.1.1f.tar.gz 
cd openssl-1.1.1f 
CROSS_COMPILE="x86_64-w64-mingw32-" 
./Configure mingw64 no-asm -shared --prefix=/opt/toolchain/openssl/install-x86_64 
make 
make install
```
##### setup3 git n2n source code
```
cd ~ 
git clone https://github.com/ntop/n2n 
cd n2n 
git checkout 3.0-stable
```
##### setup4  modify cmake file
```
cd ~/n2n 
vim toolChain.cmake #add flow content
```
SET(CMAKE_SYSTEM_NAME Windows)

SET(CMAKE_CROSSCOMPILING TRUE)

SET(CMAKE_CROSSCOMPILER "x86_64-w64-mingw32-")

SET(CMAKE_C_COMPILER "${CMAKE_CROSSCOMPILER}gcc")

SET(CMAKE_CXX_COMPILER "${CMAKE_CROSSCOMPILER}g++")

SET(CMAKE_FIND_ROOT_PATH /opt/toolchain/openssl/install-x86_64)

SET(CMAKE_VERBOSE_MAKEFILE on)

##### setup5 make
```
mkdir build 
cd build 
cmake -DCMAKE_TOOLCHAIN_FILE=../toolChain.cmake .. 
make
```
