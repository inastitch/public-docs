# Quick start
> You got a box containing the parts for an ``inastitch`` demo? You are at the right place.

## Introduction
This page describes how to connect together the different parts of the ``inastitch`` demo.

This is the final result:
![](pics/overview.jpg)

![](pics/block_diag.png)

### Shipping hardware
The demonstration hardware is made of:
 - 3 [Raspberry Pi](https://www.raspberrypi.org) 3 single-board computers and 3 camera
 - 1 [Mikrotik](https://mikrotik.com) switch/router
 - 1 [Raspberry Pi](https://www.raspberrypi.org) 4 single-board computer for the stitcher
 - 1 HDMI 8" wide screen
 - 1 USB numpad

You should also have received:
 - 1 HDMI dongle

### Shipping software
Each camera system is fitted with an micro SD-card containing an identical software image.
The stitcher has a different software image. If you happen to remove the SD-cards, be careful not to mix them.

> The demo was delivered with a very early version of ``inastitch`` for testing purposes (e.g., check that the camera or display are not damaged).

## 3-camera system

![](pics/overview1.jpg)

Power and network cables were disconnected to prevent any connector damage during shipping.

### Power
**(A)** connect each of the 3 Raspberry Pi to the USB power adapter.

### Network
**(B)** connect each of the 3 Raspberry Pi to the Ethernet switch.

### Mains
- **(C)** connect the Ethernet switch to mains (100-240V).
- **(D)** connect the USB power adapter to mains (100-240V).

## Stitcher board and display
### Stitcher
![](pics/overview2.jpg)

- **(A)** connect the stitcher Ethernet to the switch.
- **(B)** connect the stitcher USB-C power input to the USB power adapter.

### Display
![](pics/overview3.jpg)

- **(A)** connect the HDMI cable to the stitcher using the adapter.
  - Note: the stitcher has 2 HDMI outputs, it does not matter which is used, as long as only one is used.
- **(B)** connect USB power to the stitcher or the USB power adapter.
  - Note: the display board has two micro-USB connector: be careful to the connect the one for USB power (the other one is for touchscreen only).

### Numpad
![](pics/overview4.jpg)

 - **(A)** connect the USB cable to the stitcher.

Numpad keys:
 - ``Enter`` (Entrée): run OpenCV calibration with current video frames to make new transformation
   - Note: the calibration can fail when the amount of matching features is too low. Debug images are available over DLT. See the end of this page for instructions. If calibration failed, use ``Backspace``.
   - > Stitching calibration is meant to be carried out in a special environment, and is unlikely to work well in an office environment. The camera were setup for high-framerate and narrow field-of-view, in order to better record a few meters ahead of a car. In this setup, camera overlap is not sufficient when objects that are very close. For a better calibration, the scene should contain visible details, uniformly located. Please avoid white walls.
 - ``Backspace`` (<-): reload saved transformation
 - ``Star`` (\*): save current transformation
 - ``Slash`` (/): no transformation
 - ``Zero`` (0): Pause/Unpause rendering
 - ``One`` (1): Enable/Disable "frame time" overlay
   - Note: use the pause function if overlay is refreshing too fast.

## Smartphone and VLC
The Ethernet switch includes a WiFi hotspot. Connect to the SSID ``InatechDemo`` on 5G WiFi (there is no password). Once connected, open the following link with Android VLC:

    rtsp://10.42.0.1:8554/inastitch

![](pics/android_vlc.jpg)

**Note**:
 - Multiple clients can connect to the same RTSP link.
 - The delay of the stream displayed in VLC is caused by VLC which is buffering 1000ms of video by default.

### Other players
RTSP stream can be opened with many different video players.

#### ``ffmpeg``

    ffplay rtsp://10.42.0.1:8554/inastitch

#### ``gstreamer``

    gst-launch-1.0 rtspsrc location=rtsp://10.42.0.1:8554/inastitch drop-on-latency=true use-pipeline-clock=true do-retransmission=false latency=0 ! rtpjpegdepay ! jpegparse ! jpegdec ! fpsdisplaysink sync=false text-overlay=true

Note: this ``gstreamer`` command-line is configured for low-latency playback.

## Next
> You got the demo working? Congratulation!

Additional topics:
 - [**Howto** read DLT traces from camera and stitcher?](../howto/dlt/)
 - [**Howto** measure PTP clock delay with oscilloscope?](../howto/oscilloscope_and_ptp/)
 - [**Howto** analyze Ethernet traffic with WireShark?](../howto/wireshark_and_mirroring/)
 - [**Howto** update demo software?](../howto/software_update/)

Suggestions of what to show with the demo:
 - Camera frame delay below 100us (*TODO*)
   - Use overlay to display frame time and pause rendering on a quickly moving object (e.g., spinning fan).
 - Camera software PLL improving with PTP clock sync improving (*TODO*)
   - Use DLT live trace to show PTP delay beside PLL delay, right after cold start and during PTP stabilization.
 - Stitching at 60fps (and more?) (*TODO*)
   - Disable stitcher output stream and reach max 60fps. Show higher fps is possible. The camera itself is capturing at 100fps.
 
