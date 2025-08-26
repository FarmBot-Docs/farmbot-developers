---
title: "Sidecar Hardware"
slug: "sidecar-hardware"
description: "Add additional specialized hardware to your FarmBot"
---

Although FarmBot OS supports plug-and-play USB webcams, it is not possible to install additional camera drivers on FarmBot OS. FarmBot OS only supports plug-and-play cameras, and it's very important to point out that although FarmBot OS is a Linux-powered Raspberry Pi, it is not intended to be used in the same manner as a Desktop machine where end users are free to add and remove the software components running on the machine. This means that FarmBot OS is not capable of directly running specialized cameras intended for scientific or specialized use (most consumer-grade USB webcams are fine, though). FarmBot OS has a read-only filesystem and does not use the same Raspberry Pi Linux distribution that desktop Linux users are used to.

In situations where you need to install special drivers or Python modules, we recommend adding a "sidecar" hardware module to the FarmBot. The sidecar computer would be a second Raspberry Pi (or similar) that is completely under your control and which does not run FarmBot OS. You would install Raspberry Pi OS on the sidecar and follow the directions provided by most tutorials found online.

Once the sidecar is configured, there are a number of ways you can support interaction between the FarmBot's CPU and the sidecar:

 * **[Library control](#library-control)**: If the device has a reasonably reliable internet connection, you can have the sidecar talk to FBOS via [Python](../../python/intro.md) or [FarmBotJS](../farmbot-js.md). This is the easiest option.
 * **[Lua UART](#lua-uart)**: You can run a serial line from the FarmBot to the sidecar and use the Lua [UART helpers](../../lua/functions/uart.md) to send messages between the devices.
 * **[GPIO pin binding](#gpio-pin-binding)**: The sidecar can trigger a "pin binding" which activates a sequence on FBOS whenever the sidecar pulls a GPIO line high.
 * **[Lua HTTP](#lua-http)**: You could create an HTTP server that resides on the sidecar module and [make HTTP calls from Lua code in a sequence](../../lua/functions/api.md#httpparams).

 The sidecar module could then upload the photos to the FarmBot API, or you could store them on a completely different server that has higher storage limits than what the Web App provides. You could also perform image manipulation tasks directly on the sidecar.

 Other methods may be possible.

# Examples

`random()` is used here as a placeholder for the custom code you may run on your sidecar hardware.

## Library control

### Python

_on sidecar hardware (Python):_
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

_on FarmBot:_

The lighting peripheral is controlled.

See the [FarmBotPy library docs](../../python/intro.md) for additional usage instructions.

## Lua UART

_on sidecar hardware (Arduino):_
```c
void setup() {
  Serial.begin(115200);
}

void loop() {
  int randNum = random(1, 11);
  Serial.println(randNum);
  delay(1000);
}
```

_on FarmBot (Lua sequence step):_
```lua
my_uart, error = uart.open("ttyUSB0", 115200)

if error then
    toast(inspect(error), "error")
    return
end

if my_uart then
    string, error2 = my_uart.read(15000)
    if error2 then
        toast(inspect(error2), "error")
    else
        toast(inspect(string))
    end
    my_uart.close()
end
```

See the [Lua UART docs](../../lua/functions/uart.md) for additional usage instructions.

## GPIO pin binding

_on sidecar hardware (Arduino):_
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

_on FarmBot:_

The pin binding for the pin connected to the sidecar hardware is triggered.

See the [Pin Binding docs](https://software.farm.bot/docs/pin-bindings) for additional usage instructions.

## Lua HTTP

_on sidecar hardware (Python):_
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
    value = int(np.mean(gray) + random())
    return str(value)


if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

_on FarmBot (Lua sequence step):_

Where `192.168.0.100` is the local network IP address of the sidecar hardware.

```lua
local value_url = "http://192.168.0.100:5000"
toast("processing...")
local response = http{url=value_url}
local value = tonumber(response.body)
toast("processing complete. result: " .. value)
```

See the [Lua HTTP docs](../../lua/functions/api.md) for additional usage instructions.
