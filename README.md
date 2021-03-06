Arduino-LMIC proof-of-concept library
=====================================
This repository contains the IBM LMIC (LoraMAC-in-C) library, slightly
modified to run in the Arduino environment, allowing using the SX1272
LoRa tranceiver with an Arduino.

This repository is just a proof-of-concept to send data between two
SX1272 modules. It is not intended as a complete library and was not
tested in a full LoraWAN setup with a gateway (though feel free to fork
it and turn it into one if you want).

If you want to actually use this code, note that it contains version 1.4
of the library, but there are newer versions available already. Also,
the LMIC library needs to be modified to not invert IQ signals, in order
to allow device-to-device communication as used in the raw.ino example,
at the same time breaking device-to-gateway communication.

If you need device-to-device communication, make sure you reapply commit
7561aa74c (Do not invert I/Q signals to allow communication between
nodes), which was reverted in master.

At this time, this code needs an hourly build of the Arduino IDE (or
1.6.6 once it is released), since that enables C99 code to be compiled.

Connections
-----------
Note that the SX1272 module runs at 3.3V and likely does not like 5V on
its pins, so make sure to use a level shifter, or an Arduino running at
3.3V (this library was tested using a Pinoccio, which is an Arduino-like
board running at 3.3V). The evaluation board has 100 ohm resistors in
series with all data lines that might prevent damage, but I would not
count on that.

The pins to use are shown (and can be changed) in the pinmap in example
.ino files. It seems that connecting RST is not needed, and RXTX output on the
Arduino side (which controls the RX/TX antenna switch) can be connected
to the antenna switch (pin FEM\_CTX on the evaluation board).
Alternatively, you can connect the RXTX pin of the SX1272 directly to
the antenna switch (by connecting RXTX and FEM\_CTX together on the
evaluation board, or moving R2 to R1). I'm not sure why you wouldn't
always want this connection to be made, but apparently there is a reason
to control the switch from the Arduino instead of from the SX1272.

License
-------
The source files in this repository are made available under the Eclipse
Public License v1.0, except for the examples which use a more liberal
license. Refer to each individual source file for more details.

