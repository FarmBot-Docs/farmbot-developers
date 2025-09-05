---
title: "Sidecar Hardware"
slug: "sidecar-hardware"
description: "Add additional specialized hardware to your FarmBot"
---

While FarmBot OS supports plug-and-play USB webcams, it is not possible to install additional camera drivers or other software onto FarmBot OS that may be required by specialized cameras.

{%
include callout.html
type="info"
content="While FarmBot OS is a Linux-powered Raspberry Pi, it is not intended to be used in the same manner as a desktop computer where end users are free to add and remove the software components. FarmBot OS has a read-only filesystem and does not use the same Raspberry Pi Linux distribution that desktop Linux users are used to."
%}

In situations where you need to install special drivers or Python modules, we recommend using **sidecar hardware**. Sidecar hardware is a second computer, typically a Raspberry Pi (or similar), that is completely under your control and which does not run FarmBot OS. You would install [Raspberry Pi OS](https://www.raspberrypi.com/software/operating-systems/) on the sidecar and follow the directions provided by tutorials found online to run your custom software and hardware. A sidecar may also be another Arduino, a cloud-based server, or even your laptop.

Once the sidecar is configured, there are a number of ways you can support interaction between the FarmBot's CPU and the sidecar:

 * **[Python library control](#python-library-control)**: If the device has a reasonably reliable internet connection, you can have the sidecar talk to FBOS via [Python](../../python/intro.md) or [FarmBotJS](../farmbot-js.md). This is the easiest option.
 * **[Lua UART](#lua-uart)**: You can run a serial line from the FarmBot to the sidecar and use the Lua [UART helpers](../../lua/functions/uart.md) to send messages between the devices.
 * **[GPIO pin binding](#gpio-pin-binding)**: The sidecar can trigger a [pin binding](https://software.farm.bot/docs/pin-bindings) which activates a sequence on FBOS whenever the sidecar pulls a GPIO line high.
 * **[Lua HTTP](#lua-http)**: You could create an HTTP server that resides on the sidecar module and [make HTTP calls from Lua code in a sequence](../../lua/functions/api.md#httpparams).

In the case of using a 3rd party camera system, the sidecar could be triggered to take a photo by the FarmBot, and then the sidecar could upload the photos to the FarmBot API, or you could store them on a completely different server that has higher storage limits than what the Web App provides. You could also perform image manipulation tasks directly on the sidecar.

# Python library control

In this example your Python code could be run from another Raspberry Pi, a laptop, or even a cloud-based server and it will communicate with the FarmBot over the Internet.

_On sidecar hardware (Python):_

```python
from farmbot import Farmbot
from random import randint

# TOKEN = ...

fb = Farmbot()
fb.set_token(TOKEN)

fb.on(7)                     # Turn ON pin 7 (LED strip)
seconds = randint(1, 10)
fb.wait(seconds * 1000)      # Wait for a random number of seconds
fb.off(7)                    # Turn OFF pin 7 (LED strip)
```

_On FarmBot:_

The lighting peripheral is controlled.

{%
include callout.html
type="info"
content="See the [FarmBotPy library docs](../../python/intro.md) for additional usage instructions."
%}

# Lua UART

In this example you would connect an Arduino or other UART device to a spare USB port on the FarmBot's Raspberry Pi. Make sure to use [uart.list()](../../lua/functions/uart.md#uartlist) first to check which device is your sidecar.

_On sidecar hardware (Arduino):_

```c
void setup() {
  Serial.begin(115200);
}

void loop() {
  Serial.println("Hello from the sidecar!");
  delay(1000);
}
```

_On FarmBot (Lua sequence step):_

```lua
my_uart, error = uart.open("ttyUSB0", 115200)

if error then
    toast(error, "error")
    return
end

if my_uart then
    string, error2 = my_uart.read(15000)
    if error2 then
        toast(error2, "error")
    else
        toast(string)
    end
    my_uart.close()
end
```

{%
include callout.html
type="info"
content="See the [Lua UART docs](../../lua/functions/uart.md) for additional usage instructions."
%}

# GPIO pin binding

In this example, you must connect a physical wire between an output pin on your sidecar and one of FarmBot's GPIO pins. You must then configure a [pin binding](https://software.farm.bot/docs/pin-bindings) to execute a sequence or action when triggered.

_On sidecar hardware (Arduino):_

```c
int i = 0;
int randNum;
const int outPin = 7;

void setup() {
  pinMode(outPin, OUTPUT);
}

void loop() {
  randNum = random(1, 11);
  if (i == randNum) {
    digitalWrite(outPin, HIGH);
    delay(1000);
    digitalWrite(outPin, LOW);
    i = 0;
  }
  i++;
}
```

_On FarmBot:_

The pin binding for the pin connected to the sidecar hardware is triggered and the assigned sequence or action is executed.

# Lua HTTP

In this example your Python code could be run from another Raspberry Pi or your laptop on the same network as the FarmBot.

_On sidecar hardware (Python):_

```python
from flask import Flask
import cv2
import numpy as np
from random import random

app = Flask(__name__)


@app.route('/', methods=['GET'])
def capture_and_return_value():
    cap = cv2.VideoCapture(0)
    ret, frame = cap.read()
    cap.release()

    if not ret:
        return 'error'

    # process image and return result
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    value = int(np.mean(gray))
    return str(value)


if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

_On FarmBot (Lua sequence step):_

Where `192.168.0.100` is the local network IP address of the sidecar hardware.

```lua
local value_url = "http://192.168.0.100:5000"
toast("processing...")
local response = http{url=value_url}
local value = tonumber(response.body)
toast("processing complete. result: " .. value)
```

{%
include callout.html
type="info"
content="See the [Lua HTTP docs](../../lua/functions/api.md) for additional usage instructions."
%}
