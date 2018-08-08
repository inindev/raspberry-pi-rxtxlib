# RXTX Java Native Interface Library for the Raspberry Pi 

Following this documentation, a working RXTX library for the Raspberry Pi was created: http://rxtx.qbang.org/wiki/index.php/Installation_on_Linux

The binaries found in the ```rxtx-2.2pre2_arm-bins``` directory were built on 8/7/2018 using a Raspberry Pi 3 running Debian Stretch 4.14 and Java 8 (javac 1.8.0_65).

For those wanting to compile for themselves, here are the step-by-step commands used:

```
wget http://rxtx.qbang.org/pub/rxtx/rxtx-2.2pre2.zip
mkdir raspberry-pi-rxtxlib
cd raspberry-pi-rxtxlib
git init
unzip ../rxtx-2.2pre2.zip
git add .
git commit -m "downloaded from http://rxtx.qbang.org/pub/rxtx/rxtx-2.2pre2.zip"
cd rxtx-2.2pre2

# support JDK 7+
#   ./configure - lines 22097, 22019: 1.3 -> 1.7
git add ./configure
git commit -m "support JDK 7+"

# add ttyACM support
#   ./src/gnu/io/RXTXCommDriver.java - line 580: "ttyACM",
git add ./src/gnu/io/RXTXCommDriver.java
git commit -m "add support for ttyACM"

./configure
make

# expected build break (ignore as per article)
#   ./src/I2CImp.c:135:25: error: 'UTS_RELEASE' undeclared (first use in this function)

mkdir -p ../rxtx-2.2pre2_arm-bins/libs
cp ./RXTXcomm.jar ../rxtx-2.2pre2_arm-bins
cp -P ./armv7l-unknown-linux-gnu/.libs/*.so ../rxtx-2.2pre2_arm-bins/libs
```
