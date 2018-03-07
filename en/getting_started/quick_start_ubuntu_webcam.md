# Quickstart Guide — Ubuntu Camera

This Quickstart shows how to build CSD on Ubuntu LTS 16.04 (with support for MAVLink and Avahi) and connect to any supported cameras (or webcams) that are attached to Ubuntu. 

1. Install the [Core](#core_deps) and [Avahi](#avahi_deps) pre-requisites:
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
   ```
1. Get the CSD source code by cloning the the [camera-streaming-daemon](https://github.com/intel/camera-streaming-daemon) repo (or your fork):
   ```sh
   git clone https://github.com/intel/camera-streaming-daemon.git
   cd camera-streaming-daemon
   git submodule update --init --recursive
   ```
1. Configure CSD with support MAVLink and Avahi:
```
./autogen.sh && ./configure --enable-mavlink --enable-avahi
```
1. Build CSD:
   ```
   make
   ```
1. Attach supported cameras to Ubuntu.
   > **Note** Any camera that supports the [Video4Linux (V4L2) API](https://linuxtv.org/downloads/v4l-dvb-apis/uapi/v4l/v4l2.html) should be automatically detected. Some readily-available cameras that are known to work are: *Logitech C270 HD Webcam*, *Sony PlayStation Eye Camera*, *Intel RealSense*.
1. Run CSD specifying Ubuntu [configuration file](../getting_started/building_installation.md#configuration-file-runtime).
   ```
   ./csd -c samples/files/ubuntu.conf
   ```

Then run the [Sanity Tests](../test/sanity_tests.md) to verify that CSD is working correctly.
