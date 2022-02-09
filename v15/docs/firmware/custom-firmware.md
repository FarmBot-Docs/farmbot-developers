---
title: "Custom Firmware"
slug: "custom-firmware"
---

* toc
{:toc}

If you do not want to use the firmware installed by FarmBot OS, you can still install custom firmware using one of the methods below.

# custom.hex firmware

1. Power down FarmBot.
2. Remove the microSD card and insert it into your computer.
3. Copy your `custom.hex` firmware file to the drive that shows up.
4. Eject the microSD card and put it back into FarmBot.
5. Power back on.
6. FarmBot will use the custom firmware until the file is deleted.

# Arduino IDE

1. Download and install the [Arduino IDE](https://www.arduino.cc/en/Main/Software) onto your computer.
2. Download and unzip the latest [FarmBot Arduino Firmware](https://github.com/FarmBot/farmbot-arduino-firmware).
3. In the firmware folder you just unzipped, go to the **src** sub-folder and open up **src** with the Arduino IDE. Note: this file is blank, but there are many other file tabs that should be automatically opened as well.
4. Connect your Arduino to your computer with a USB cable.
5. From the IDE, click **Tools** > **Board**, and then select `Arduino Mega 2560`.
6. Now click **File** > **Upload**. This will flash the firmware onto your Arduino.
