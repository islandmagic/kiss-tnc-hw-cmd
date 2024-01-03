# KISS TNC Hardware Specific Commands

This is an attempt to documente the known KISS TNC hardware specific commands.

In the definition of the [KISS TNC protocol](https://www.ax25.net/kiss.aspx), command `0x06` is reserved for hardware specific extensions.

|Command|Function|Device|Parameter|Returns|
|---|---|---|---|---|
|0xEA|Set Frequency|[^1]|32 bit frequency in Hz. MSB first|NA|
|0xEB|Restore Frequency|[^1]|NA|NA|
||Too many to list|[^2] [^3]|||

[^1]: [PicoAPRS](http://www.db1nto.de/)
[^2]: [Mobilinkd 3](https://github.com/mobilinkd/tnc3-firmware/blob/master/TNC/KissHardware.hpp)
[^3]: [Mobilinkd 4](https://github.com/mobilinkd/tnc4-firmware/blob/master/Core/TNC/KissHardware.hpp)
