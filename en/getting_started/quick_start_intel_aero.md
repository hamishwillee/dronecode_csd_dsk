# Quickstart Guide — Intel Aero

This Quickstart provides turnkey instructions for building CSD on Ubuntu LTS 16.04 (with support for Realsense, Aero bottom facing camera, MAVLink and Avahi) and then deploy it to Intel Aero. 

## Build CSD

To build CSD:
1. Install the [Core](#core_deps), [Avahi](#avahi_deps) and [RealSense](#realsense_deps) pre-requisites listed above:
   ```sh
   sudo apt-get update -y
   sudo apt-get install git autoconf libtool python-pip -y
   sudo apt-get install gstreamer-1.0 \
       libgstreamer-plugins-base1.0-dev \
       libgstrtspserver-1.0-dev -y
   ## Required python packages
   sudo pip2 -q install -U future
   # Avahi
   sudo apt-get install libavahi-client-dev libavahi-core-dev libavahi-glib-dev -y
   # RealSense
   echo 'deb "http://realsense-alm-public.s3.amazonaws.com/apt-repo" xenial main' | sudo tee /etc/apt/sources.list.d/realsense-latest.list
   sudo apt-key adv --keyserver keys.gnupg.net --recv-key D6FB2970 
   sudo apt update -y
   sudo apt-get install librealsense-dev -y
   ```
1. Get the CSD source code by cloning the the [camera-streaming-daemon](https://github.com/intel/camera-streaming-daemon) repo (or your fork):
   ```sh
   git clone https://github.com/intel/camera-streaming-daemon.git
   cd camera-streaming-daemon
   git submodule update --init --recursive
   ```
1. Configure CSD with the normal Aero settings:
   ```
   ./autogen.sh && ./configure --enable-aero --enable-mavlink --enable-avahi
   ```
1. Build CSD for Aero:
   ```
   make
   ```
   
## Deploy CSD to Aero

[Deploy CSD to Aero](https://github.com/intel/camera-streaming-daemon/wiki/Deploying-on-Aero) explains how to add CSD to the *Intel Aero* image. 
* *csd* must be placed in **/usr/bin**. 
* The [aero.conf](https://github.com/intel/camera-streaming-daemon/blob/master/samples/files/aero.conf) file must be placed in **/etc/csd**.
* The *csd.service* file must be copied to **/lib/system/system** (see [Autostart CSD](../guide/autostart.md)).

## Verify Installation

1. Make sure CSD is running (Aero starts CSD on boot):
   ```sh
   systemctl status csd
   ```
1. Run the [Sanity Tests](sanity_tests.md) to verify that CSD is working correctly.

