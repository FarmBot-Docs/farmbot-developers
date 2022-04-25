---
title: "Firmware"
slug: "firmware"
description: "Executes g-code like commands over a serial line to move the FarmBot and operate its peripherals. [GitHub repository](https://github.com/FarmBot/farmbot-arduino-firmware)."
---

The **firmware** runs on an Arduino microcontroller and is written in C++. The firmware is usually flashed to the Arduino via FarmBot OS.

{%
include callout.html
type="warning"
title="Internally used commands"
content="The commands and responses on this page are used for communication between [FarmBot OS](farmbot-os.md) and the [FarmBot Arduino Firmware](https://github.com/FarmBot/farmbot-arduino-firmware). Outside of that internal communication, commands on this page can only be sent by disconnecting the Arduino from the Raspberry Pi and connecting a USB cable from a computer directly to the Arduino.

FarmBot OS communication via the [Message Broker](../docs/message-broker.md) consists of higher-level [CeleryScript](celery-script.md) commands, not the commands listed on this page."
%}

# Sending commands

Commands are sent to the Arduino using the command code and number, any arguments (separated by spaces), and a CR/NL (`\r\n`).

For example, to set parameter number `101` to `1`, you would send `F22 P101 V1\r\n`, where `F22` is the write parameter command, `P101` is the parameter argument, `V1` is the value argument, and `\r\n` is the CR/NL.

For this example, the firmware will respond with (comments excluded):
```
R08 *F22 P101 V1*     // the command received (echo)
R01 Q0                // command started
R21 P101 V1 Q0        // report parameter 101 value: 1
R02 Q0                // command finished successfully
```

The `Q` at the end of the responses designates the command queue number. `Q` + a number can be appended to any command sent and the responses will include the same `Q` number provided.

Commands that can be sent begin with `G` or `F`. Responses and status reports received from the Arduino begin with `R`.

|General command responses     |Description                   |
|------------------------------|------------------------------|
|R08                           |Echo
|R09                           |Invalid
|R01                           |Started
|R04                           |Running
|R02                           |Finished successfully
|R03                           |Finished with error
|R07                           |Movement retry

|Idle and status responses     |Description                   |
|------------------------------|------------------------------|
|R00                           |Ready
|R87                           |Locked
|R88                           |Config not approved (use `F22 P2 V1` to approve manually)

# Emergency stop

|Command |Description                   |
|--------|------------------------------|
|E       |Emergency stop
|R87     |Locked
|F09     |Reset emergency stop (unlock)

# Movement

|Movement reports              |X                             |Y                             |Z                             |
|------------------------------|------------------------------|------------------------------|------------------------------|
|R81: report endstops          |XA: end stop 1 (0/1)<br>XB: end stop 2 (0/1)|YA: end stop 1 (0/1)<br>YB: end stop 2 (0/1)|ZA: end stop 1 (0/1)<br>ZB: end stop 2 (0/1)
|R82: current position (mm)    |X                             |Y                             |Z
|R84: encoder position (mm)    |X                             |Y                             |Z
|R85: encoder position (edges) |X                             |Y                             |Z
|timeout                       |R71                           |R72                           |R73
|R05: axis state               |X0: idle<br>X1: starting motor<br>X2: accelerating<br>X3: cruising<br>X4: decelerating<br>X5: stopping motor<br>X6: crawling|Y0: idle<br>Y1: starting motor<br>Y2: accelerating<br>Y3: cruising<br>Y4: decelerating<br>Y5: stopping motor<br>Y6: crawling|Z0: idle<br>Z1: starting motor<br>Z2: accelerating<br>Z3: cruising<br>Z4: decelerating<br>Z5: stopping motor<br>Z6: crawling

## Move to

|G00: Move to location                                |X  |Y  |Z  |
|-----------------------------------------------------|---|---|---|
|__axis location__<br>_unit:_ mm<br>_default:_ 0      |X  |Y  |Z
|__speed__<br>_unit:_ steps/s<br>_default:_ max speed |A  |B  |C

__Examples:__

```text
// Move to (0, 0, 0) at normal speed
G0

// Move to (100, 200, 300) at normal speed
G00 X100 Y200 Z300

// Move to (100, 200, 300) at specified axis speeds
G00 X100 Y200 Z300 A400 B500 Z600
```

|Command |Description |
|--------|------------|
|G28     |Move each axis to home (zero) in order: Z, Y, X

## Homing

Finds zero for an axis. Requires the use of encoders or end-stops. For more information, see [Calibration and Homing](https://software.farm.bot/docs/calibration-and-homing).

|Find home (zero)              |X                             |Y                             |Z                             |
|------------------------------|------------------------------|------------------------------|------------------------------|
|Command                       |F11                           |F12                           |F13
|Response: Homing complete     |R11                           |R12                           |R13

## Calibrate axis

Measures an axis length and then finds zero for that axis. Requires the use of encoders or end-stops. For more information, see [Calibration and Homing](https://software.farm.bot/docs/calibration-and-homing).

|Calibrate axis                |X                             |Y                             |Z                             |
|------------------------------|------------------------------|------------------------------|------------------------------|
|Command                       |F14                           |F15                           |F16
|Response: `R06`               |`R06 X0`: idle<br>`R06 X1`: moving to home<br>`R06 X2`: moving to end|`R06 Y0`: idle<br>`R06 Y1`: moving to home<br>`R06 Y2`: moving to end|`R06 Z0`: idle<br>`R06 Z1`: moving to home<br>`R06 Z2`: moving to end

## Zero axis

Sets zero for an axis. For more information, see [Calibration and Homing](https://software.farm.bot/docs/calibration-and-homing).

|Command                       |X                             |Y                             |Z                             |
|------------------------------|------------------------------|------------------------------|------------------------------|
|F84                           |X1: set to zero<br>X0: don't set to zero|Y1: set to zero<br>Y0: don't set to zero|Z1: set to zero<br>Z0: don't set to zero

# Pin control

|<i></i>                       |Command|Pin Number   |Value                         |Mode|
|------------------------------|-------|-------------|------------------------------|----|
|Read pin                      |F42    |P            |                              |`M0`: digital<br>`M1`: analog
|Write pin                     |F41    |P            |V (0-1 digital, 0-255 analog) |`M0`: digital<br>`M1`: analog
|Set pin input/output mode     |F43    |P            |                              |`M0`: input<br>`M1`: output<br>`M2`: input pullup
|Set servo angle<br>(only pins 4, 5, 6, and 11)|F61|P|V (0-180)                  |
|Response (report pin value)   |R41    |P            |V (0-1 digital, 0-1023 analog)|

# Pin assignment

For Arduino and Farmduino board pin assignments, see [src/pins.h](https://github.com/FarmBot/farmbot-arduino-firmware/blob/main/src/pins.h).

# What's next?

 * [Parameters](firmware/parameters.md)
 * [Custom Firmware](firmware/custom-firmware.md)
