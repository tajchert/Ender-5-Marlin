# Precompiled Marlin 2.0.5.3 for Ender 5
This is precompiled Marlin firmware for Creality Ender 5. Proceed on your own causion but this should fix issue with OctoPrint and Ender 5 (1.1.5 board) stepper motor stopping mid print on one of the axis.

## Based on:

* [2.0.5.3 Marlin firmware](https://github.com/MarlinFirmware/Marlin)
* [Configuration file by firestrife23 for Ender 5 and Marlin 1.1.x](https://github.com/firestrife23/ender-5-marlin)
* Config is changed for 800 step lead screw on Ender 5 (Z axis)
* Build using Arduino IDE
* Board config from [Lauszus](https://github.com/Lauszus/Sanguino)
* Processor was set to ATmega1284 or ATmega1284p (16MHz)
* [Post by 1970s_MonkeyKing](https://www.reddit.com/r/ender3/comments/cdlvmm/modified_marlin_119bugfix_fixes_the_s3d_print/) and [post by gekkonaut](https://www.reddit.com/r/ender5/comments/e4q3ry/yaxis_lockup_ender_5_pro_silent_board_115_marlin/) that firstly mentioned how to solve this issue.
* Firware is optimized (sizewise) using:
  
  `compiler.c.extra_flags=-fno-tree-scev-cprop -fno-split-wide-types -Wl,--relax -mcall-prologues
compiler.cpp.extra_flags=-fno-tree-scev-cprop -fno-split-wide-types -Wl,--relax -mcall-prologues
compiler.c.elf.extra_flags=-Wl,--relax` based on [this post](http://www.do-it-neat.com/install-marlin-1-1-9-at-your-creality-ender-5/) which results in 92% device memory used instead of 96% with not optimized build.

## Use:

You should be ready to load firware with or without bootloader from folder `precompiled firmware` using OctoPrint.
For OctoPrint you need to install `avrdude` and plugin `Firmware Updated`, and later set path to avrdude (ex. `/usr/bin/avrdude`), AVR MCU to `ATmega1284p` and AVR Programmer Type to `arduino`. Connection set same baud rate as on main page of Octoprint in "connection" section. Enable post-flas gcode with `M502;M500`.
In my case I had to call additionaly `M502` and `M500` (due to "Err: EEprom version on Ender display") reboot and `G28` (homing after flash). 


## TODO:

* Check if there is any better Configuration file out there
* Automatize releases and triggers if possible compiling firmware based on new Marlin releases in the cloud so it is automatic and always up to date.
* Set home to top-right corner as currently it goes to bottom left after the print.
