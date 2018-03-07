# Deploying on Aero

Last available image for Aero doesn't have all dependencies to run Camera-Streaming-Daemon. In order to test it it is necessary to build the Aero image from master branch.

## Build an updated Aero image

Follow instructions on [meta-intel-aero > Quickstart > get-sources](https://github.com/intel-aero/meta-intel-aero/wiki/Quickstart-Guide#get-sources) in order to get Aero sources. After running `repo sync` command checkout the master branch in meta-intel-aero directory.

```
cd meta-intel-aero
git checkout intel-aero/master
cd ..
```

After that, keep following the guide from: [meta-intel-aero > Quickstart > set-environment](https://github.com/intel-aero/meta-intel-aero/wiki/Quickstart-Guide#set-environment) to build and flash the image.

Now it is necessary to boot Aero board and set up an ssh connection with your computer, following information on https://github.com/intel-aero/meta-intel-aero/wiki/Functionality#wi-fi

## Copy camera-streaming-daemon to Aero board

After building camera-streaming-daemon following information on [Quickstart — Intel Aero](../getting_started/quick_start_intel_aero.md), copy the binary to the board:
```
scp camera-streaming-daemon 192.168.1.1:
```

## Run camera-stream-daemon

Connect to the Aero and run the daemon:
```
ssh 192.18.1.1
./camera-streaming-daemon
```

## Test it

Daemon running on drone can be tested using same approaches described in:
* [Sanity Tests](../test/sanity_tests.md)
* [Manual Testing](../test/README.md)
 
