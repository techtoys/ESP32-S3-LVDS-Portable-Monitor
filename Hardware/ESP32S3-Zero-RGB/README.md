# Preliminary PCB design of a ESP32-S3 + RA8889 graphic controller

## Patches:

* Previously I used 8080 16-bit to drive RA8889. It works but there is a fatal problem : no 8080 data read in ESP32 i80 driver but RA8889 NEEDS data read to use DMA Serial Flash read/write and various niche features. Unwillingly I switched to 4-wire SPI mode with a much slower performance!
* To set SPI interface, XPS[2:0] of RA8889 set 101 by strip wires
* XTEST[2:1] in 00 in normal mode. A jumper "glued" to XTEST[2:1] to 01 to force SPI master I/F pin floating. Need to do this when new graphic media is downloaded to Serial Flash by an external programmer
* LED backlight circuit with AP3031KTR needs revision. L50 (4.7uH) and D50 (SD103AWS) need higher ratings
* J50's Pin38,39 removed from RA8889's XKIN0_SCL and XKOUT0_SDA. Re-route to GPIO36(SCL) and GPIO35(SDA) of ESP32-S3

