# Dronecode Camera Server SDK

[![Build Status](https://travis-ci.org/intel/camera-streaming-daemon.svg?branch=master)](https://travis-ci.org/intel/camera-streaming-daemon)
<a href="https://scan.coverity.com/projects/01org-camera-streaming-daemon">
  <img alt="Coverity Scan Build Status"
       src="https://scan.coverity.com/projects/12056/badge.svg"/>
</a>

The Dronecode Camera Server (a.k.a., *Camera Streaming Daemon* - CSD) is an extensible Linux camera server for interfacing cameras with the Dronecode platform. 

It can connect to multiple cameras and provides access to them via the [MAVLink Camera Protocol](https://mavlink.io/en/protocol/camera.html) and RTSP video streams. It can also advertise available RTPS streams and interact with Gazebo to provide access to a camera running within a simulation.

> **Tip** The daemon is the easiest way for Camera OEMs to interface with the Dronecode platform. Many cameras will just work "out of the box". At most, OEMs may need to implement a camera integration layer.


## Forums and Chat {#support}

The core development team and community are active on the following chat channel:

* [Slack](http://slack.px4.io) (sign up)


## Reporting Bugs & Issues

If you have any problems using CSD first post them on the [support channels above](#support).

If directed by the development team, issues may be raised on [Github here](https://github.com/intel/camera-streaming-daemon/issues).


## Contributing

The [Contributing Guide](contribute/README.md) explains the contribution model and the main areas where you can help.


## Licence

The *Camera Streaming Daemon* source code is free to use and modify under terms of the permissive
[Apache License 2.0](https://github.com/intel/camera-streaming-daemon/blob/master/LICENSE).

This documentation is licensed under *CC BY 4.0* ([Human readable overview](https://creativecommons.org/licenses/by/4.0/) | [LICENSE](https://github.com/hamishwillee/dronecode_csd_sdk/blob/master/LICENSE)).
