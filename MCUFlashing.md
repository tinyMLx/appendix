## "Flashing" Code to a Microcontroller

You may be interested to learn a bit more about what’s happening in the process of deploying code to a microcontroller. The exact method will vary between MCU, but there are two main constructs that you’ll hear abou: in-system programming and bootloaders. In the case of the Nano 33 BLE Sense, when we upload code over USB, we are relying on a bootloader to accept the incoming program. 

### In-System Programming (ISP)

This approach does **not** require that there be anything pre-existing on the MCU to initiate transfer to program memory (which is not only desirable, but necessary for initial controller setup), but requires the use of an external programmer that can be costly and interfaces with the MCU via various standards:
+ A few popular standards include: [ICSP](https://en.wikipedia.org/wiki/In-system_programming), [SWD](https://en.wikipedia.org/wiki/JTAG#Similar_interface_standards), [PDI](https://en.wikipedia.org/wiki/AVR_microcontrollers#Programming_interfaces), [JTAG](https://en.wikipedia.org/wiki/JTAG).
+ The etymology for ISP relates to the notion of updating device software or firmware for an embedded MCU within its application environment

### Bootloaders

In contrast, bootloaders specifically call on (really, are, rather) existing software that persists in memory and will, on reset, listen for signals that a new program is inbound.
+ If there is new code available, the incoming program overwrites the existing code but preserves the bootloader so that this process can be repeated
+ If there is not new code available, the existing code (as applicable) begins
+ Unlike various forms of ISP, the Arduino bootloader is generally accessible via USB, although technically some boards require USB-to-UART translation 
+ Notably, a double tap of the small white reset button on top of the Nano 33 BLE Sense will draw the MCU away from any existing program into the bootloader, at times resolving issues where uploads are blocked or otherwise inhibited by the existing program. 
