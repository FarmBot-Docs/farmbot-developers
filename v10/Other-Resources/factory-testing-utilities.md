---
title: "Factory Testing Utilities"
slug: "factory-testing-utilities"
---

* toc
{:toc}

Every electronics box is tested at the factory to ensure all of the stepper drivers, peripheral circuits, LEDs, and buttons are functional. We currently have two test `.img` files, one for Genesis electronics and one for Express electronics. Follow the instructions below to conduct a test.

# Setup
  1. Flash the `express.img` or `genesis.img` file to a **microSD card** and insert it into the **Pi**. [Download here](https://github.com/FarmBot-Labs/farmbot-factory-test-firmware/releases).
  2. Plug all **motors**, **encoders**, **peripherals**, **LED indicator lights**, and **buttons** into the **Farmduino** and **Pi adapter board** when applicable.
  3. Plug in the **power supply**. The Pi will begin booting and flash firmware to the Arduino. This will take about 40 seconds on the Pi Zero and 20 seconds on the Pi 3. Once ready, the E-stop button's LED will turn on <span class="fa fa-circle led red"></span> (solid red).

# Running the tests
## Express

|Activation Method             |Expected Action               |
|------------------------------|------------------------------|
|Plugging in the power should...|Turn on the E-stop button's LED <span class="fa fa-circle led red"></span> (solid red) once the device has fully booted (about 40 seconds after plugging in power).
|Pressing the E-stop button should...|Turn on all peripherals for 0.2s and then turn them off
|Pressing the E-stop button should...|Move all motors forward by 3/4 of a revolution and then backwards by 3/4 of a revolution

## Genesis

|Activation Method             |Expected Action               |
|------------------------------|------------------------------|
|Plugging in the power should...|Turn on the E-stop button's LED <span class="fa fa-circle led red"></span> (solid red) once the device has fully booted (about 20 seconds after plugging in power)
|Pressing the E-stop button should...|Turn on the Unlock button's LED <span class="fa fa-circle led orange"></span> (solid orange)
|Pressing the Unlock button should...|Turn on Button 3's LED <span class="fa fa-circle-thin led gray"></span> (solid white)
|Pressing Button 3 should...   |Turn on Button 4's LED <span class="fa fa-circle-thin led gray"></span> (solid white)
|Pressing Button 4 should...   |Turn on Button 5's LED <span class="fa fa-circle-thin led gray"></span> (solid white)
|Pressing Button 5 should...   |Turn on the Sync LED Indicator <span class="fa fa-circle led green"></span> (solid green), the Connectivity LED Indicator <span class="fa fa-circle led blue"></span> (solid blue), and LED Indicators 3 and 4 <span class="fa fa-circle-thin led gray"></span> (solid white)
|Pressing any button should... |Turn on all peripherals for 0.2s and then turn them off
|Pressing any button should... |Move all motors forward by 3/4 of a revolution and then backwards by 3/4 of a revolution



{%
include callout.html
type="info"
title="If a test fails..."
content="If one of the encoder or peripheral load detection tests fail, then the device will flash all button LEDs and LED Indicators <span class=\"fa fa-sun-o led red\"></span><span class=\"fa fa-sun-o led orange\"></span><span class=\"fa fa-sun-o led green\"></span><span class=\"fa fa-sun-o led blue\"></span><span class=\"fa fa-sun-o led gray\"></span>. Pressing any button will reset the device back to the first test."
%}

