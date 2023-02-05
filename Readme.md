# emonTx V3 3-phase Firmware

This sketch is a development of the 3-phase ‘discrete sample’ sketch and MartinR’s PLL
energy diverter.

It is intended for use on a **3-phase, 4-wire system**. It utilises advanced
features of the Atmel328P microprocessor to provide continuous monitoring of voltage of
one phase and the currents in all three phases, thereby allowing a good estimate of real
power to be calculated. The physical quantities are measured continuously, the average
values are calculated and transmitted at user-defined intervals.

Pulse counting and temperature monitoring using a single DS18B20 sensor is supported.

*By [Robert Wall](https://community.openenergymonitor.org/u/robert.wall/summary)*

## Key Feautures

- Continuous monitoring of one voltage channel and up 4 current channels.
- Gives an accurate measure of rapidly varying loads.
- 1800 sample sets per second – using 4 channels of an emonTx V3.4 @ 50 Hz
- Calculates rms voltage, rms current, real & apparent power & power factor.
- Pulse input for supply meter monitoring.
- Integrated temperature measurement (one DS18B20 sensor).
- User-defined reporting interval.
- Suitable for operation on a three-phase, 4-wire supply at 50 or 60 Hz.
- Can be calibrated for any voltage and current (default calibration is for emonTx with 100 A CTs & UK a.c. adapter).

## My Modifications
- Set `EMONESP` as default radio (9600 baud)
- `vCal` set to fit bell transformer [Kanlux KTF-8-24](https://www.kanlux.com/en/product/23260/KTF-8-24) on ~8VAC terminals
- `i1Cal` - `i4Cal` set to 30A CT transformers instead of 100A
- Extended serial output for another parameters: 
    - **vrms** - Voltage (V RMS)
    - **frq** - Frequency (Hz)
    - **irms1** - Current L1 (A RMS)
    - **irms2** - Current L2 (A RMS)
    - **irms3** - Current L3 (A RMS)
    - **irms4** - Current CT4 (A RMS)
    - **ct1** - Real Power L1 (A)
    - **ct2** - Real Power L2 (A)
    - **ct3** - Real Power L3 (A)
    - **ct4** - Real Power CT4 (A)
    - **act1** - Apparent Power L1 (W)
    - **act2** - Apparent Power L2 (W)
    - **act3** - Apparent Power L3 (W)
    - **act4** - Apparent Power CT4 (W)
    - **pf1** - Power Factor L1
    - **pf2** - Power Factor L2
    - **pf3** - Power Factor L3
    - **pf4** - Power Factor CT4
    - **power** - Real Power Total (W)
    - **apower** - Apparent Power Total (W)
    - **t1** - Temperature (1-wire DS18B20)
    - **pulses** - Pulse Count

## Limitations

Because the voltage of only one phase can be measured, the sketch must assume that
the voltages of the other two phases are the same. This will, in most cases, not be true,
therefore the powers calculated and recorded will be inaccurate. However, this error
should normally be limited to a few percent. Voltage imbalance might be the result of
unbalanced loads within your installation, or it might result from the actions of other
consumers on the same supply.

If you find that one or other phase voltage is consistently wrong, you might want to
consider a small adjustment to the current calibration of the affected phase.
Because of the additional power required for continuous operation, a 5 V USB power
supply is likely to be required, even if only the on-board RFM69CW radio is used. The 5 V
power will always be required when the ESP8266 WiFi module is added.

The sketch is not compatible with the RFM12B radio module, nor the Arduino Due.


***

## Resources

### [Introduction to three-phase](https://learn.openenergymonitor.org/electricity-monitoring/ac-power-theory/3-phase-power)

### [Full 3-phase Firmware User Guide](emontx-3-phase-userguide.pdf)
*Including calibration instructions*

## Required Hardware

- emonTx V3.4
- 3 x Clip on CT sensors
- 1 x AC-AC adapter
- USB to UART programmer (to upload firmware)

## Upload pre compiled

- Firmware can be uploaded directly using [arduino-xloader](https://www.hobbytronics.co.uk/arduino-xloader) tool to grab latest compiled release and upload via serial.

or

- Download pre-compiled `.hex` from [this github](https://github.com/stanoba/emontx-3phase/tree/master/compiled) and upload using avrdude

Depending on your ISP

`avrdude  -uV -c arduino -p ATMEGA328P -P /dev/ttyUSB0 -b 115200 -U flash:w:firmware.hex`


## Compile & Upload

- Firmware can be compiled and uploaded with PlatformIO, see [User Guide](https://guide.openenergymonitor.org/technical/compiling)

Or

- Arduino IDE
