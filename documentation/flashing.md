# Flashing

The software for the power supply module can be found in the
[CARL Air Brake Power Supply Software][cab-psup-sw-repo] repository. This
repository contains two programs - a calibration program, and a main program -
that can be flashed onto the board. The calibration program is used to calibrate
the voltage thresholds at which the indication LEDs should turn red. The main
program is used to monitor the battery voltage and drive the LEDs as described
in [description.md][des]. For detailed instructions for flashing the software,
see [CARL Air Brake Power Supply Software][cab-psup-sw-repo].

[des]:              ./description.md

[cab-psup-sw-repo]: https://github.com/Kenneth-Goveas/CARL-Air-Brake-Power-Supply-Software
