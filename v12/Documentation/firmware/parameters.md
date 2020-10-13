---
title: "Parameters"
slug: "parameters"
---

* toc
{:toc}

# Writing parameters
To write a parameter, send an `F22 P V` command, where `P` is the parameter number and `V` is the parameter value.

# Reading parameters
To read parameters, use one of the following two commands.

|Action                        |Command                       |Parameter Number              |
|------------------------------|------------------------------|------------------------------|
|Report all parameters         |F20                           |
|Read parameter                |F21                           |P

The firmware will respond in the format `R21 P V`, where `P` is the parameter number and `V` is the parameter value.

# List of parameters
The firmware uses the following parameters, as found in the code repository at [src/ParameterList.h](https://github.com/FarmBot/farmbot-arduino-firmware/blob/main/src/ParameterList.h).

## General

|ID                            |Name                          |Description                   |
|------------------------------|------------------------------|------------------------------|
|0                             |`PARAM_VERSION`               |Version number of the parameter set
|1                             |`PARAM_TEST`                  |Used for diagnostics
|2                             |`PARAM_CONFIG_OK`             |Set when the firmware is sufficiently configured

## Movements

|ID                            |Name                          |Description                   |
|------------------------------|------------------------------|------------------------------|
|4                             |`PARAM_E_STOP_ON_MOV_ERR`     |Determines wether or not the firmware should emergency stop upon movement error
|5                             |`PARAM_MOV_NR_RETRY`          |Number of times to retry a movement before stopping with error
|11<br>12<br>13                |`MOVEMENT_TIMEOUT_X`<br>`MOVEMENT_TIMEOUT_Y`<br>`MOVEMENT_TIMEOUT_Z`|Time in seconds before a movement along an axis times out and stops with error

## Motors

|ID                            |Name                          |Description                   |
|------------------------------|------------------------------|------------------------------|
|15<br>16<br>17                |`MOVEMENT_KEEP_ACTIVE_X`<br>`MOVEMENT_KEEP_ACTIVE_Y`<br>`MOVEMENT_KEEP_ACTIVE_Z`|Determines if motors should remain powered when idle
|31<br>32<br>33                |`MOVEMENT_INVERT_MOTOR_X`<br>`MOVEMENT_INVERT_MOTOR_Y`<br>`MOVEMENT_INVERT_MOTOR_Z`|Reverses the direction a motor spins when moving in both the positive and negative directions
|36                            |`MOVEMENT_SECONDARY_MOTOR_X`  |Enables the use of a second X-axis motor
|37                            |`MOVEMENT_SECONDARY_MOTOR_INVERT_X`|Inverts the rotation of the second X-axis motor
|51<br>52<br>53                |`MOVEMENT_HOME_UP_X`<br>`MOVEMENT_HOME_UP_Y`<br>`MOVEMENT_HOME_UP_Z`|Determines which direction the bot must move to reach the home (zero) position
|55<br>56<br>57                |`MOVEMENT_STEP_PER_MM_X`<br>`MOVEMENT_STEP_PER_MM_Y`<br>`MOVEMENT_STEP_PER_MM_Z`|Determines the steps/mm scaling factor

## Motor speeds

|ID                            |Name                          |Description                   |
|------------------------------|------------------------------|------------------------------|
|41<br>42<br>43                |`MOVEMENT_STEPS_ACC_DEC_X`<br>`MOVEMENT_STEPS_ACC_DEC_Y`<br>`MOVEMENT_STEPS_ACC_DEC_Z`|Number of steps used to accelerate along an axis
|61<br>62<br>63                |`MOVEMENT_MIN_SPD_X`<br>`MOVEMENT_MIN_SPD_Y`<br>`MOVEMENT_MIN_SPD_Z`|Minimum speed in steps/second
|71<br>72<br>73                |`MOVEMENT_MAX_SPD_X`<br>`MOVEMENT_MAX_SPD_Y`<br>`MOVEMENT_MAX_SPD_Z`|Maximum speed in steps/second
|65<br>66<br>67                |`MOVEMENT_HOME_SPEED_X`<br>`MOVEMENT_HOME_SPEED_Y`<br>`MOVEMENT_HOME_SPEED_Z`|Homing and calibrating speed in steps/second

## Endpoints

|ID                            |Name                          |Description                   |
|------------------------------|------------------------------|------------------------------|
|25<br>26<br>27                |`MOVEMENT_ENABLE_ENDPOINTS_X`<br>`MOVEMENT_ENABLE_ENDPOINTS_Y`<br>`MOVEMENT_ENABLE_ENDPOINTS_Z`|Enables the use of endstop hardware such as limit switches
|21<br>22<br>23                |`MOVEMENT_INVERT_ENDPOINTS_X`<br>`MOVEMENT_INVERT_ENDPOINTS_Y`<br>`MOVEMENT_INVERT_ENDPOINTS_Z`|Inverts which endstop represents the maximum and minimum locations along an axis
|75<br>76<br>77                |`MOVEMENT_INVERT_2_ENDPOINTS_X`<br>`MOVEMENT_INVERT_2_ENDPOINTS_Y`<br>`MOVEMENT_INVERT_2_ENDPOINTS_Z`|Changes the type of limit switch being used from NO to NC
|45<br>46<br>47                |`MOVEMENT_STOP_AT_HOME_X`<br>`MOVEMENT_STOP_AT_HOME_Y`<br>`MOVEMENT_STOP_AT_HOME_Z`|Determines if the bot is allowed to move past the minimum/home (zero) position
|145<br>146<br>147             |`MOVEMENT_STOP_AT_MAX_X`<br>`MOVEMENT_STOP_AT_MAX_Y`<br>`MOVEMENT_STOP_AT_MAX_Z`|Determines if the bot is allowed to move past the maximum position
|141<br>142<br>143             |`MOVEMENT_AXIS_NR_STEPS_X`<br>`MOVEMENT_AXIS_NR_STEPS_Y`<br>`MOVEMENT_AXIS_NR_STEPS_Z`|Size of an axis in steps (lower byte)
|151<br>152<br>153             |`MOVEMENT_AXIS_NR_STEPS_H_X`<br>`MOVEMENT_AXIS_NR_STEPS_H_Y`<br>`MOVEMENT_AXIS_NR_STEPS_H_Z`|Size of an axis in steps (higher byte)

## TMC2130 stepper drivers

|ID                            |Name                          |Description                   |
|------------------------------|------------------------------|------------------------------|
|81<br>82<br>83                |`MOVEMENT_MOTOR_CURRENT_X`<br>`MOVEMENT_MOTOR_CURRENT_Y`<br>`MOVEMENT_MOTOR_CURRENT_Z`|Sets the current in milliamps
|85<br>86<br>87                |`MOVEMENT_STALL_SENSITIVITY_X`<br>`MOVEMENT_STALL_SENSITIVITY_Y`<br>`MOVEMENT_STALL_SENSITIVITY_Z`|Sets the amount of back emf required to trigger a stall
|91<br>92<br>93                |`MOVEMENT_MICROSTEPS_X`<br>`MOVEMENT_MICROSTEPS_Y`<br>`MOVEMENT_MICROSTEPS_Z`|Sets the number of microsteps per step

## Encoders

|ID                            |Name                          |Description                   |
|------------------------------|------------------------------|------------------------------|
|101<br>102<br>103             |`ENCODER_ENABLED_X`<br>`ENCODER_ENABLED_Y`<br>`ENCODER_ENABLED_Z`|Enables the use of rotary encoders
|105<br>106<br>107             |`ENCODER_TYPE_X`<br>`ENCODER_TYPE_Y`<br>`ENCODER_TYPE_Z`|Sets the type of encoder being used (single ended or differential)
|111<br>112<br>113             |`ENCODER_MISSED_STEPS_MAX_X`<br>`ENCODER_MISSED_STEPS_MAX_Y`<br>`ENCODER_MISSED_STEPS_MAX_Z`|Sets the maximum number of steps an encoder can deviate from the expected count before determining a stall has occurred
|115<br>116<br>117             |`ENCODER_SCALING_X`<br>`ENCODER_SCALING_Y`<br>`ENCODER_SCALING_Z`|Determines the scaling factor between encoder steps and motor steps
|121<br>122<br>123             |`ENCODER_MISSED_STEPS_DECAY_X`<br>`ENCODER_MISSED_STEPS_DECAY_Y`<br>`ENCODER_MISSED_STEPS_DECAY_Z`|Sets the amount the missed encoder step count should decrease by with each recorded step
|125<br>126<br>127             |`ENCODER_USE_FOR_POS_X`<br>`ENCODER_USE_FOR_POS_Y`<br>`ENCODER_USE_FOR_POS_Z`|Determines if the controller should continue moving based on the position as reported by the encoders
|131<br>132<br>133             |`ENCODER_INVERT_X`<br>`ENCODER_INVERT_Y`<br>`ENCODER_INVERT_Z`|Reverses the direction the encoder must rotate to count in each direction

## Pin guard

|ID                            |Name                          |Description                   |
|------------------------------|------------------------------|------------------------------|
|201<br>202<br>203             |`PIN_GUARD_1_PIN_NR`<br>`PIN_GUARD_1_TIME_OUT`<br>`PIN_GUARD_1_ACTIVE_STATE`|Pin guard 1 pin number, timeout (in seconds), and active state (low or high)
|205<br>206<br>207             |`PIN_GUARD_2_PIN_NR`<br>`PIN_GUARD_2_TIME_OUT`<br>`PIN_GUARD_2_ACTIVE_STATE`|Pin guard 2 pin number, timeout (in seconds), and active state (low or high)
|211<br>212<br>213             |`PIN_GUARD_3_PIN_NR`<br>`PIN_GUARD_3_TIME_OUT`<br>`PIN_GUARD_3_ACTIVE_STATE`|Pin guard 3 pin number, timeout (in seconds), and active state (low or high)
|215<br>216<br>217             |`PIN_GUARD_4_PIN_NR`<br>`PIN_GUARD_4_TIME_OUT`<br>`PIN_GUARD_4_ACTIVE_STATE`|Pin guard 4 pin number, timeout (in seconds), and active state (low or high)
|221<br>222<br>223             |`PIN_GUARD_5_PIN_NR`<br>`PIN_GUARD_5_TIME_OUT`<br>`PIN_GUARD_5_ACTIVE_STATE`|Pin guard 5 pin number, timeout (in seconds), and active state (low or high)

## Deprecated

{%
include callout.html
type="warning"
title=""
content="The following parameters are no longer used, though support for them may still remain in the firmware."
%}



|ID                            |Name                          |Description                   |
|------------------------------|------------------------------|------------------------------|
|3                             |`PARAM_USE_EEPROM`            |
|18<br>19<br>20                |`MOVEMENT_HOME_AT_BOOT_X`<br>`MOVEMENT_HOME_AT_BOOT_Y`<br>`MOVEMENT_HOME_AT_BOOT_Z`|Deprecated

