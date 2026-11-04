# USB-C Power Breakout

A small breadboard-friendly board that takes power from any USB-C charger and provides regulated **5 V** and **3.3 V** outputs, with a power indicator LED. Designed in KiCad as my first PCB.

> Status: 🛠️ In progress — schematic stage

## Features
- USB-C input that works with USB-C-to-C chargers (5.1 kΩ CC pull-downs)
- 3.3 V output, up to 600 mA (AP2112K-3.3 LDO)
- 5 V pass-through output
- Power-on LED
- 0805 passives for easy hand soldering

## Block diagram
<!-- Add an image: docs/block-diagram.png -->
`USB-C → (5 V rail) → LED indicator`
`               └──→ AP2112K LDO → (3.3 V rail)`
`Both rails + GND → pin header`

## Schematic
<!-- Export from KiCad: File → Plot → PDF, save to docs/schematic.pdf, and add a PNG here -->

## PCB
<!-- Add 3D view render and front/back photos -->

## Bill of materials
| Ref | Part | Value / Package | Qty |
|---|---|---|---|
| J1 | USB-C receptacle | power-only | 1 |
| R1, R2 | Resistor | 5.1 kΩ, 0805 | 2 |
| R3 | Resistor | 1 kΩ, 0805 | 1 |
| D1 | LED | red, 0805 | 1 |
| U1 | LDO regulator | AP2112K-3.3, SOT-23-5 | 1 |
| C1, C2 | Capacitor | 1 µF, 0805 | 2 |
| J2 | Pin header | 1x03, 2.54 mm | 1 |

## What I learned / problems I hit 
<!-- Fill this in as you go. This is the section recruiters actually read. -->
- Making a clean power supply
- starting with "USB_C_Receptacle_PowerOnly_6P"
- VBUS: The 5v coming from charger
- GND: Ground
- CC1, CC2: Handshake pins
- SHIELD: metal shell of connector.

- power led
-   lights up whenever 5v is present
-   if resistor wasn't there it would burn out

- 3.3v regulator, less power 
-   takes 5v in and holds it at 3.3v
-   ap2112k is a LDO, constantly adjusts voltage to keep output at 3.3v
-   dropped voltage turns to heat - a tradeoff
-   EN: regulator only runs when EN is high, tying to VIN means it switches on when power arrives.
- The two µF capacitors
-   C2: tiny energy reserve - covers sudden current demands the USB cable can't respond to fast enough (VIN stabilization) 
-   C1: keeps regulator stable & smooths 3.3v output when load changes.
- Output Header (J2)
-   +5v - for 5v devices 
-   +3v3 - devices such as ESP32 or RP2040
-   GND - return path for both

- 5v pin is raw usb power, 3.3 is more regulated.



## Testing
<!-- Measured output voltages, which chargers it worked with, etc. -->

## Files
- `usbc-power-breakout.kicad_sch` — schematic
- `usbc-power-breakout.kicad_pcb` — PCB layout
- `fabrication/` — Gerbers sent to the fab (added once ordered)

## Tools
KiCad · Multimeter · Soldering station
