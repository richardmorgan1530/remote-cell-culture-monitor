# Camera Mapping

This document explains how USB cameras are mapped to Motion
configuration files in the Remote Cell Culture Monitor system.

Multi-camera Raspberry Pi setups often encounter problems where camera
device numbers (e.g. /dev/video0, /dev/video1) change after reboot. To
prevent this, this project uses persistent device paths from
/dev/v4l/by-path/.

These paths are stable because they correspond to the physical USB port
location on the Raspberry Pi rather than the order in which cameras are
detected.

------------------------------------------------------------------------

# Why Stable Device Paths Are Important

If cameras are configured using:

/dev/video0
/dev/video1
/dev/video2

The numbering may change after:

-   rebooting the Raspberry Pi
-   unplugging and reconnecting cameras
-   connecting additional USB devices

This can cause cameras to appear in the wrong position in the monitoring
interface.

Using /dev/v4l/by-path avoids this issue because each path corresponds
to a specific USB controller port.

------------------------------------------------------------------------

# Identify Camera Device Paths

List available video devices:

ls /dev/video\*

List persistent device paths:

ls -l /dev/v4l/by-path

Example output:

platform-xhci-hcd.1-usb-0:1:1.0-video-index0 -\> ../../video0
platform-xhci-hcd.1-usb-0:2:1.0-video-index0 -\> ../../video1
platform-xhci-hcd.0-usb-0:2:1.0-video-index0 -\> ../../video2
platform-xhci-hcd.0-usb-0:3:1.0-video-index0 -\> ../../video3

These entries correspond to specific physical USB ports.

------------------------------------------------------------------------

# Camera Mapping Used in This Project

Camera 1 → Top Left → Port 8081 
Camera 2 → Bottom Left → Port 8082
Camera 3 → Top Right → Port 8083 
Camera 4 → Bottom Right → Port 8084

Each camera is configured in a separate Motion thread configuration
file.

thread1.conf → Camera 1 
thread2.conf → Camera 2 
thread3.conf → Camera 3
thread4.conf → Camera 4

------------------------------------------------------------------------

# Example Thread Configuration

video_device
/dev/v4l/by-path/platform-xhci-hcd.1-usb-0:1:1.0-video-index0

width 640 
height 480 
framerate 15

stream_port 8081

This ensures the camera remains mapped correctly even if /dev/videoX
numbers change.

------------------------------------------------------------------------

# Verify Camera Mapping

To confirm cameras are mapped correctly:

1.  Start Motion
2.  Open each camera stream

Example:

http://`<raspberry-pi-ip>`{=html}:8081
http://`<raspberry-pi-ip>`{=html}:8082
http://`<raspberry-pi-ip>`{=html}:8083
http://`<raspberry-pi-ip>`{=html}:8084

Verify that each stream corresponds to the expected camera position.

------------------------------------------------------------------------

# Troubleshooting

Camera not detected:

lsusb

Check video devices:

ls /dev/video\*

Device path missing:

ls -l /dev/v4l/by-path

------------------------------------------------------------------------

# Notes

USB hubs may change device paths depending on topology.

For maximum stability connect cameras directly to Raspberry Pi USB ports
when possible.
