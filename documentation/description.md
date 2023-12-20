# Description

The CARL Air Brake computer is comprised of the following three circuit boards.
These boards are loaded with their respective software and connected by stacking
on top of each other, to make up the computer.

- Peripheral devices module.
- Power supply module.
- Raspberry Pi 3 model A+.

This repository contains the electronic design for the second of the above three
boards. Other electronic designs and software are contained in different
repositories (for more details, see [CARL Air Brake][cab-repo]).

## Overview

The power supply module supplies regulated power to all systems in the CARL Air
Brake computer. Additionally, it also monitors the battery voltage and indicates
the same on an LED array. When the battery is fully charged, all these LEDs
light up in green. As the voltage drops, they turn red one by one. Below a
critically low voltage, they also start flashing to indicate to the user that
the battery needs charging. The board also contains status LEDs to indicate
which of the onboard power lines are live.

## Battery

The power supply module is intended for use with a lithium polymer battery with
the following specifications.

| **Specification**             | **Value** |
| ----------------------------- | --------- |
| Cells in series               | 3         |
| Nominal voltage               | 11.1V     |
| Fully charged voltage         | 12.6V     |
| Continuous discharge current  | >1.5A     |

## Components

The relevant circuit components on the board are marked on the following diagram
and described below.

![Relevant components of the power supply module](
  ./images/relevant_components.png
)

| **Designation** | **Description**                                       |
| --------------- | ----------------------------------------------------- |
| J1              | Screw terminal for battery connection.                |
| J2              | Port for ICSP cable for programming.                  |
| J3              | Port for USB cable for programming.                   |
| J4              | Stacking header for connecting other boards.          |
| J5              | Header for supplying 6V to peripheral devices module. |
| SW1             | Switch for making/breaking battery connection.        |
| D6-D10          | Battery voltage indication LEDs.                      |
| D11-D14         | Power line status LEDs.                               |
| TP1-TP6         | Test points for measuring power line voltages.        |

## Working

The following is a simple block diagram of the power supply module.

![Block diagram of the power supply module](
  ./images/block_diagram.png
)

As seen in the above diagram, the board contains the following five power lines.
Note that the line voltages listed below are nominal values. It is normal for
the actual voltages to deviate slightly.

| **Name**  | **Description**                           | **Voltage**     |
| --------- | ----------------------------------------- | --------------- |
| VBAT      | Positive terminal of battery.             | Battery voltage |
| +3.3V     | Output of 3.3V regulator on Raspberry Pi. | 3.3V            |
| +5V       | Output of onboard 5V regulator.           | 5V              |
| +6V       | Output of onboard 6V regulator.           | 6V              |
| VMCU      | Power line for onboard microcontroller.   | 5V              |

When the battery is connected and the switch turned on, the VBAT, VMCU, +5V, and
+6V lines become live. If, in addition to the battery, the Raspberry Pi is also
connected, then the +3.3V line also becomes live. If any or both of the two
programming cables are connected, the VMCU line becomes live regardless of
whether or not the battery is connected. Thus, the VMCU line has three power
sources - the battery, and two programming cables. It is safe to simultaneously
connect more than one of these power sources as the board has protection diodes
that will prevent any short circuit.

The Raspberry Pi draws power from the +5V line. The Raspberry Pi has an onboard
3.3V regulator which supplies power to the +3.3V line. The peripheral devices
module draws power from the +3.3V, +5V, and +6V lines. The VMCU line supplies
power to the onboard microcontroller of the power supply module, and its
associated circuitry. Each regulated power line is also connected to a separate
status LED (D11-D14) to visually indicate which lines are live. Additionally,
all power and GND lines are connected to separate test points (TP1-TP6) for
measuring their voltages with a multimeter.

The onboard microcontroller is programmable from the two ports J2 and J3. When
flashed with the appropriate software (see [flashing.md][fsh]), it measures the
battery voltage and accordingly drives the indication LEDs (D6-D10), resulting
in the behavior described in [Overview](#overview).

[fsh]:      ./flashing.md

[cab-repo]: https://github.com/Kenneth-Goveas/CARL-Air-Brake
