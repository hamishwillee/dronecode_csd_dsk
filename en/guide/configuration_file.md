# CSD Configuration File

CSD loads a configuration file with custom options/settings when it is started.

> **Tip** The [samples/files](https://github.com/intel/camera-streaming-daemon/tree/master/samples/files) directory contains sample configuration files that you can use for Ubuntu, Aero and other platforms. 

By default CSD will look for a configuration file in **/etc/csd/main.conf**. You can over-ride this file location using the `CSD_CONF_FILE` environment variable or with the `-c` switch when starting CSD.

The headings below explain the structure and main sections of the configuration file (see also [samples/files/config.sample](https://github.com/intel/camera-streaming-daemon/blob/master/samples/files/config.sample)).


## Config File Structure

The configuration file is composed of sections, each containing *keys* and *values*. For example:
```
[section-name]
someKey=someValue
aDifferentKey=anotherValue

[anothersection]
...

```

> **Tip** The keys/values are case insensitive (i.e. `Key=Value` is the same as `key=value`). By convention lower case is used.

## Expected Sections

The following sections, along with key/value definitions, are likely to be present in most configuration files. 

### [gstreamer]

Key | Description | Default
-- | --- | ---
`muxer` | Muxer used to create the gstreamer pipeline. | rtpjpegpay
`encoder` | Muxer used to create the gstreamer pipeline. | jpegenc
`converter` | Converter used to create the gstreamer pipeline. | videoconvert

Example:
```
[gstreamer]
muxer=rtph264pay
encoder=x264enc
converter=autovideoconvert
```


### [v4l2]

Key | Description | Default
-- | --- | ---
`blacklist` | Comma separated list of `/dev/video` devices that won't be exported by CSD. For example, if the video streams from cameras `/dev/video123` and `/dev/video456` could not be exported you would set: `blacklist = video123,video456`.| <empty>

Example:
```
[v4l2]
blacklist=video10
```

### [mavlink]

Key | Description | Default
-- | --- | ---
`port` | MAVLink destination UDP port. | 14550
`broadcast_addr` | Broadcast address to send MAVLink heartbeat messages. | 255.255.255.255
`rtsp_server_addr` | IP address or hostname of the interface where the RTSP server is running. This is the address that will be used by the client to make the RTSP request. | 0.0.0.0
`system_id` | System ID of the CSD to be used in MAVLink communications. | 42
`component_id` | Component ID of the CSD to be used in MAVLink communications. | 100 (MAV_COMP_ID_CAMERA)

Example:

Gazebo/Ubuntu
```
[mavlink]
port=24550
broadcast_addr=127.0.0.255
rtsp_server_addr=127.0.0.1
system_id=1
```

Aero
```
[mavlink]
port=80550
broadcast_addr=127.0.0.255
rtsp_server_addr=127.0.0.1
system_id=2
```


### [uri]

Key | Description | Default
-- | --- | ---
`<camera-device-id>` | URI for the [Camera Definition File](https://mavlink.io/en/protocol/camera_def.html) of the camera device <camera-device-id> | -

> **Note** The [MAVLink Camera Protocol](https://mavlink.io/en/protocol/camera.html) expects cameras to supply the URL for a [Camera Definition File](https://mavlink.io/en/protocol/camera_def.html) that contains camera capability/setting parameters. The location of this file is supplied to the CSD in this section using the device id. 

Example:

Gazebo
```
[uri]
video0=http://127.0.0.1/camera-def-R200rgb.xml
video1=http://127.0.0.1/camera-def.xml
gazebo=http://127.0.0.1/camera-def-R200rgb.xml
```

Aero
```
[uri]
video13=http://127.0.0.1/camera-def-R200rgb.xml
video1=http://127.0.0.1/camera-def.xml
video02=dummy
```

Ubuntu
```
[uri]
video0=http://127.0.0.1/camera-def-R200rgb.xml
video1=http://127.0.0.1/camera-def.xml
video02=dummy
gazebo=http://127.0.0.1/camera-def-R200rgb.xml
```

### [imgcap]

Key | Description | Default
-- | --- | ---
`location` | The local path with write permission where captured images will be saved (usually the system-standard "Temp" directory) | -

Example:
```
[imgcap]
location=~/Temp/
```


### [gazebo]

Key | Description | Default
--- | --- | ---
`camtopic` | Gazebo topic where camera images are published. | -

Example:
```
[gazebo]
camtopic=~/typhoon_h480/cgo3_camera_link/camera/image
```