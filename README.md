Single Channel LoRaWAN Gateway
==============================
This repository contains a proof-of-concept implementation of a single
channel LoRaWAN gateway. It has been tested on the Wemos D1 Mini, using a 
Semtech SX1276 transceiver (HopeRF RFM95W).

The code is for testing and development purposes only, and is not meant 
for production usage. 

Engine is based on code base of Single Channel gateway for RaspberryPI
which is developed by Thomas Telkamp. Code was ported and extended to run
on ESP 8266 mcu and provide RTC, Webserver and DNS services.

Maintained by Maarten Westenberg (mw12554@hotmail.com)

Features
--------
- listen on configurable frequency and spreading factor
- Works from SF7 to SF12. However, when using OTAA the TTN system reacts different: 
	For SF7 and S&8 the system will reply in RX1 time slot and use the same SF setting.
	For SF9-SF12 the TTN system will reply with SF12 (even when the node requests with SF9).
	This makes OTAA usage for single channel gateways more difficult than ever, 
	as the gateway should cheat the TTN system and reply with its SFx setting no matter what 
	the TTN server will reply with.
- status updates sent every 30 seconds
- can forward to two UDP backend servers
- DNS support for server lookup
- NTP Support for time sync with internet time servers
- Webserver support (default port 8080)

Not (yet) supported:
- PACKET_PUSH_ACK processing
- SF7BW250 modulation
- FSK modulation
- downstream messages (tx)

Dependencies
------------

- gBase64 library, The gBase library is actually a base64 library made 
	by Adam Rudd (url=https://github.com/adamvr/arduino-base64). I changed the name because I had
	another base64 library installed on my system and they did not coexist well.
- Time library (http://playground.arduino.cc/code/time)

Connections
-----------
See http://things4u.github.io in the hardware section for building
and connection instructions

Configuration
-------------

Defaults:

- LoRa:   SF9 at 868.1 Mhz
- Server: 54.229.214.112, port 1700  (The Things Network: croft.thethings.girovito.nl)
  or directly croft.thethings.girovito.nl

Edit .h file (ESP-sc-gway.h) to change configuration (look for: "Configure these values!").

Please set location, email and description.

License
-------
The source files in this repository are made available under the Eclipse
Public License v1.0, except for the base64 implementation, that has been
copied from the Semtech Packet Forwader.
