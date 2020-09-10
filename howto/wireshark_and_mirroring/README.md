# WireShark and port mirroring
## Introduction
Ethernet traffic can be analyzed with WireShark. The network traffic of one switch port can be mirrored on another port.
It is then convenient to connect a laptop to a free switch port and capture the traffic.

## Mikrotik switch config
Via the web-interface, go to "Terminal" (see *top-right* corner), and type the following command to copy all the traffic from ``ether4`` onto ``ether1``:

    /interface ethernet switch
    set switch1 mirror-source=ether4 mirror-target=ether1

## WireShark
This is an example of traffic from a camera streaming ``RTP/JPEG``:

*TODO*

### WireShark and AVTP

*TODO*
