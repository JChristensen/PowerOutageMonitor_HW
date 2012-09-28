ReadMe file for Arduino-Based Power Outage Logger board v1.1
https://github.com/JChristensen/PowerOutageLogger_HW
Jack Christensen Sep 2012

This work is licensed under the Creative Commons Attribution-ShareAlike 3.0
Unported License. To view a copy of this license, visit
http://creativecommons.org/licenses/by-sa/3.0/ or send a letter to Creative
Commons, 171 Second Street, Suite 300, San Francisco, California, 94105, USA.

================================================================================
This repository contains the following for the Power Outage Logger board:

Schematic
Eagle Files
Bill of materials (below)

An Arduino sketch for the board can be found at:
https://github.com/JChristensen/PowerOutageLogger_SW

================================================================================
Assembly notes and options

1. The board is intended to be powered by either a 5V or a 7-12V AC adapter.
When using a 5V adapter, it MUST BE REGULATED; in this case, C1, C2, D1 and U2
do not need to be installed. Set the PWR SEL jumper (JP1) to DIRECT when using a
5V regulated adapter.

2. When disconnected from the power, certain 5V regulated adapters may emit a
power blip that the RTC interprets as a power-up event. This results in the
power-down and power-up timestamps being identical even if the power is left off
for several minutes. To eliminate this, power the RTC from an MCU pin by
selecting MCU power via the RTC PWR jumper (JP2). This is supported by the
sketch referenced above. It is also recommended to set the ATmega328P brown-out
detector to 4.3V by setting the extended fuse byte to 0x04. Note that when the
RTC is powered from the MCU pin, any MCU reset will cause a power outage to be
logged, whether or not is is associated with an actual power outage.

3. The Tinsharp TC1602A-09T 16x2 LCD display uses an LED backlight that requires
only 15mA at 5V. This means that a current-limiting resistor is not needed (use
a jumper in place of R5), and that the backlight can be powered from an MCU pin.
Do not use displays that require more than 20mA to operate the backlight. Note
also that some displays will require a non-zero value for R5 if their backlight
operates on less than 5V.

4. The board includes optional provisions for an on-board temperature sensor and
associated dropping resistor (U3, R6). An optional three-position terminal block
can also connect to an off-board sensor. The Arduino sketch referenced above
contains no code for these optional sensors.

5. Photocell PC1 is used to adjust the display backlight brightness to match the
ambient light level. The Arduino sketch above uses the internal AVR pullup
resistor in association with PC1, but if this does not result in satisfactory
adjustment of the backlight, then the internal pullup can be disabled and an
alternate resistor can be installed at R4.

================================================================================
Power Outage Logger Board
Bill of Materials

Part    Value               Device
C1      47uF                Radial lead electrolytic, 16V, 2 mm lead spacing
C2      100nF               50V MLCC, 0.1 in. lead spacing
C3      47uF                Radial lead electrolytic, 16V, 2 mm lead spacing
C4      100nF               50V MLCC, 0.1 in. lead spacing
C5      100nF               50V MLCC, 0.1 in. lead spacing
C6      100nF               50V MLCC, 0.1 in. lead spacing
C7      100nF               50V MLCC, 0.1 in. lead spacing
C8      27pF                50V MLCC, 0.1 in. lead spacing
C9      27pF                50V MLCC, 0.1 in. lead spacing
C10     100nF               50V MLCC, 0.1 in. lead spacing
D1      1N4004              Silicon rectifier
D2      1N4148              Signal diode
D3      5mm LED
J1      2.1mm power jack
JP1     Supply select       1x3 0.1 in. male header (or use jumper)
JP2     RTC power select    1x3 0.1 in. male header, right angle (or use jumper)
JP3     FTDI                1x6 0.1 in. male header, right angle
JP4     ICSP                2x6 0.1 in. male header (OPTIONAL)
PC1     CdS Photocell
PCB1    MCP79412            MCP79412 RTC Breakout Board, see:
                            https://github.com/JChristensen/rtc79412
PCB2    TC1602A-09T         Tinsharp 16x2 LCD
R1      10K                 1/8W 5% carbon film
R2      10K                 3/8 in. square trimpot, Bourns 3386P or equivalent
R3      330?                1/8W 5% carbon film
R4      10K                 1/8W 5% carbon film,
                            OPTIONAL pullup resistor for photocell (sketch uses
                            internal AVR pullup).
R5      0?                  1/8W 5% carbon film, current-limiting resistor for
                            LCD backlight.
                            Use a jumper with the TC1602A-09T display. Use
                            appropriate value for other displays.
R6      4.7K                1/8W 5% carbon film,
                            OPTIONAL pullup resistor for temperature/external
                            sensor.
S1      SET                 Omron B3F-312X
S2      UP                  Omron B3F-312X
S3      DN                  Omron B3F-312X
S4      RESET               Omron B3F-1020 (OPTIONAL)
TB1     Ext Sensor          3.5 mm x 3 terminal block, OST-TB-33.5MM or similar,
                            OPTIONAL for external sensor connection.
U1      ATmega328P-PU       Microcontroller
U2      78L05               5V 100mA Voltage Regulator
U3      DS18B20             Temperature Sensor (OPTIONAL)
Y1      16MHz               16MHz 18pF crystal
