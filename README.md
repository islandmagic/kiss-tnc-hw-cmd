# KISS TNC Hardware Specific Commands

This is an attempt to documente the known KISS TNC hardware specific commands.

In the definition of the [KISS TNC protocol](https://www.ax25.net/kiss.aspx), command `0x06` is reserved for hardware specific extensions.

|Command|Function|Device|Parameter|Returns|
|---|---|---|---|---|
|0x28|Get Firmware Version|[^2] [^3] [^4] [^6]|NA|Version as a string|
|0x7B|Get API Version|[^2] [^3] [^4] [^6]|NA|Version as uint16|
|0x7E|Get Capabilities|[^2] [^3] [^4] [^6]|NA|Capabilities bit-field as uint16|
|0xEA|Set Frequency|[^1] [^4][^5][^6]|32 bit frequency in Hz. MSB first|NA|
|0xEB|Restore Frequency|[^1] [^4][^5][^6]|NA|NA|
|0xF4|Set Baud Rate|[^4] [^6]|uint8: 0 = 1200 baud, 1 = 9600 baud|NA|
||Too many to list|[^2] [^3]|||

[^1]: [PicoAPRS](http://www.db1nto.de/)
[^2]: [Mobilinkd 3](https://github.com/mobilinkd/tnc3-firmware/blob/master/TNC/KissHardware.hpp)
[^3]: [Mobilinkd 4](https://github.com/mobilinkd/tnc4-firmware/blob/master/Core/TNC/KissHardware.hpp)
[^4]: [B.B. Link](https://github.com/islandmagic/bb-link)
[^5]: VR-N76, UV-PRO and GA-5WB with firmware 0.7.11 or later.
[^6]: [QRV Link](https://github.com/jonnyborbs/qrv-link)

## BLE capability descriptor

Devices using the [BLE-KISS API](https://github.com/hessu/aprs-specs/blob/master/BLE-KISS-API.md) can declare which of these commands they support, so apps can detect capabilities during service discovery instead of matching on the device name.

The KISS write characteristic (`00000002-ba2a-46c9-ae49-01b0961f68bb`) carries a read-only Characteristic User Description descriptor (UUID `0x2901`). Its value is a label, a colon, then a hexadecimal capability bitmask:

```
Write KISS data:03
```

|Bit|Value|Capability|
|---|---|---|
|0|0x01|Set/Restore Frequency (`0xEA`, `0xEB`)|
|1|0x02|9600 baud (`0xF4` with parameter `1`)|

Apps read the descriptor after connecting, during service and characteristic discovery, before sending any KISS frames.
