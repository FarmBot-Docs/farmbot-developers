---
title: "Farmware"
slug: "farmware"
excerpt: "FarmBot OS plug-Ins to expand FarmBot functionality"
hidden: false
createdAt: "2018-05-16T19:40:14.748Z"
updatedAt: "2019-07-30T18:42:16.658Z"
---

__You Might Not Need a Farmware:__
**Farmware is not the only way to write custom Farmbot software.** Please see [this document](doc:you-might-not-need-farmware) for more information



__For Developers:__
This documentation is meant for Farmware developers. For use of Farmware in the Web App, see the [FarmBot Web App Farmware documentation](https://software.farm.bot/docs/farmware).



# What is Farmware?

Farmware is custom Python code that runs on the Farmbot CPU. It is useful when you need to control the device, but cannot control the device remotely due to design considerations. Farmware should only be used in cases when it would be impractical to run software remotely, such as operations that require offline support or extremely low latency.

# Example

For a complete Farmware example, see [Hello Farmware](https://github.com/FarmBot-Labs/hello-farmware). Each of the code samples below can be run as a Farmware by replacing the contents of `hello.py` in `Hello Farmware` with the copied code.

# Web App API

_Use: long term information storage_

Farmware can access FarmBot Web App database resources, such as plants, sequences, and points, via `app` actions as shown in this example:


__GET: Python API request example:__

```python
from farmware_tools import app

plants = app.get_plants()
```

__other actions:__

```python
from farmware_tools import app

tools = app.get(endpoint='tools')
points = app.search_points(search_payload={'x': 100})
plants = app.download_plants()
points = app.get_points()  # Shown as circles in the Farm Designer (weeds)
plants = app.get_plants()
toolslots = app.get_toolslots()
device_name = app.get_property(endpoint='device', field='name')
sequence_id = app.find_sequence_by_name(name='my sequence')
```

__GET example 2:__

```python
#!/usr/bin/env python

'Get specific data (such as timezone) from the FarmBot Web App.'

from farmware_tools import app

# Device timezone info (set via the dropdown in the Web App Device widget)
timezone_string = app.get_property('device', 'timezone')
tz_offset_hours = app.get_property('device', 'tz_offset_hours')

print('My device timezone is: {} (UTC{})'.format(timezone_string, tz_offset_hours))
# Example output (to FTDI): My device timezone is: America/Los_Angeles (UTC-7)
```

__legacy GET:__

```python
import os
import requests

headers = {'Authorization': 'Bearer ' + os.environ['API_TOKEN'],
           'content-type': "application/json"}
response = requests.get('https://my.farmbot.io/api/points', headers=headers)
points = response.json()
```

__legacy GET 2:__

```python
#!/usr/bin/env python

'Get specific data (such as timezone) from the FarmBot Web App.'

import os
import requests

headers = {'Authorization': 'Bearer ' + os.environ['API_TOKEN'],
           'content-type': "application/json"}
response = requests.get('https://my.farmbot.io/api/device', headers=headers)
device_data = response.json()

# Device timezone info (set via the dropdown in the Web App Device widget)
timezone_string = device_data['timezone']
tz_offset_hours = device_data['tz_offset_hrs']

print('My device timezone is: {} (UTC{})'.format(timezone_string, tz_offset_hours))
# Example output (to FTDI): My device timezone is: America/Los_Angeles (UTC-7)
```




__POST: Python API request example:__

```python
from farmware_tools import app

new_plant = app.add_plant(x=100, y=200)
```

__other actions:__

```python
from farmware_tools import app

app.patch(endpoint='device', payload={'name': 'My FarmBot'})
app.put(endpoint='device', payload={'name': 'My FarmBot'})
app.delete(endpoint='point', _id=1)
```

__legacy:__

```python
import os
import requests

headers = {'Authorization': 'Bearer ' + os.environ['API_TOKEN'],
           'content-type': "application/json"}
payload = {'pointer_type': 'Plant', 'x': 100, 'y': 200}
response = requests.post('https://my.farmbot.io/api/points',
                         headers=headers, json=payload)
new_plant = response.json()
```




__output of add_plant (new_plant):__

```json
new_plant = {
  "pointer_type": "Plant",
  "name": "Unknown Plant",
  "openfarm_slug": "not-set",
  "created_at": "2017-06-22T15:14:55.652Z",
  "updated_at": "2017-06-22T15:14:55.652Z",
  "plant_status": "planned",
  "meta": {},
  "radius": 50,
  "y": 200,
  "x": 100,
  "z": 0,
  "id": 101,
  "device_id": 1
```

For a list of available resources, see [Web App API resources](doc:rest-api#section-resource-list).

# Environment Variables

_Use: Farmware API information_

Environment variables are used to get Farmware API information and special locations.


__environment variables:__

```python
from farmware_tools import env

ENV = env.Env()
FARMBOT_OS_VERSION = ENV.fbos_version
IMAGES_DIR = ENV.images_dir
```

__legacy:__

```python
import os

API_TOKEN = os.environ['API_TOKEN']
FARMWARE_URL = os.environ['FARMWARE_URL']
FARMWARE_TOKEN = os.environ['FARMWARE_TOKEN']
IMAGES_DIR = os.environ['IMAGES_DIR']
FARMBOT_OS_VERSION = os.environ['FARMBOT_OS_VERSION']
```



# Farmware API

_Use: get information from FarmBot OS (bot state)_

The Farmware API can be used to get information such as position and pin status as shown in this example:


__bot info:__

```python
from farmware_tools import device

position_x = device.get_current_position('x')
pin_13_value = device.get_pin_value(13)

bot_state = device.get_bot_state()
```

__legacy:__

```python
import os
import requests

headers = {
  'Authorization': 'bearer {}'.format(os.environ['FARMWARE_TOKEN']),
  'content-type': "application/json"}
response = requests.get(os.environ['FARMWARE_URL'] + '/api/v1/bot/state',
              headers=headers)

bot_state = response.json()
position_x = bot_state['location_data']['position']['x']
pin_13_value = bot_state['pins']['13']['value']
```

See [FarmBotJS BotStateTree](https://github.com/FarmBot/farmbot-js/blob/master/src/interfaces.ts) for a complete list of information available in the the bot's state.

# Celery Script

_Use: real-time web app communication and bot actions_

Celery Script is JSON sent to FarmBot OS to perform actions such as device movements and setting environment variables.

Send Celery Script  via `device` actions as shown in this example:


__send message:__

```python
from farmware_tools import device

device.log('Bot is at position {{ x }}, {{ y }}, {{ z }}.', 'success', ['toast'])

# or
# device.log(message='Hello!', message_type='success', channels=['toast'])
```

__all:__

```python
from farmware_tools import device

device.log(message='hi')
device.send_message(message='hi', message_type='info')
device.calibrate(axis='x')
device.check_updates(package='farmbot_os')
device.emergency_lock()
device.emergency_unlock()
device.execute(sequence_id=1)
device.execute_script(label='take-photo')
device.run_farmware(label='take-photo')
device.factory_reset(package='farmbot_os')
device.find_home(axis='x')
device.home(axis='x')
device.install_farmware(url='https://raw.githubusercontent.com/FarmBot-Labs/hello-farmware/master/manifest.json')
device.install_first_party_farmware()
device.move_absolute(location=device.assemble_coordinate(1, 2, 3), speed=100, offset=device.assemble_coordinate(0, 0, 0))
device.move_relative(x=100, y=0, z=0, speed=100)
device.power_off()
device.read_pin(pin_number=1, label='', pin_mode=0)
device.read_status()
device.reboot()
device.remove_farmware(package='hello-farmware')
device.set_pin_io_mode(pin_number=1, pin_io_mode=0)
device.set_servo_angle(pin_number=4, pin_value=0)
device.set_user_env(key='hello_farmware_key', value='0')
device.sync()
device.take_photo()
device.toggle_pin(pin_number=1)
device.update_farmware(package='take-photo')
device.wait(milliseconds=1000)
device.write_pin(pin_number=1, pin_value=0, pin_mode=0)
device.zero(axis='x')
device.send_celery_script({'kind': 'take_photo', 'args': ''})
```

__legacy:__

```python
import os
import requests

send_message = {
  "kind": "send_message",
  "args": {
    "message": "Bot is at position {{ x }}, {{ y }}, {{ z }}.",
    "message_type": "success"
  },
  "body": [
    {
      "kind": "channel",
      "args": {
        "channel_name": "toast"
      }
    }
  ]
}


headers = {
  'Authorization': 'bearer {}'.format(os.environ['FARMWARE_TOKEN']),
  'content-type': "application/json"}
payload = send_message
requests.post(os.environ['FARMWARE_URL'] + '/api/v1/celery_script',
              json=payload, headers=headers)
```

For a list of all available actions, see the second tab of the above example code, `all`.

Also see the [Celery Script developer documentation](doc:celery-script) and [the corpus](https://github.com/FarmBot/farmbot-js/blob/master/dist/corpus.d.ts) for more information.

# Inputs

If a Farmware requires inputs, an input form can be added to the Web App Farmware page by adding the `config` field to the manifest:


__Form Building (v7):__

```json

  "package": "Farmware Name",
  // Other fields omitted for clarity (see the `Farmware manifest` section)
  "config": [
    {
      "name": "key",
      "label": "Input Name",
      "value": 10
    }
  ]
```

__v8:__

```json

  "package": "Farmware Name",
  // Other fields omitted for clarity (see the `Farmware manifest` section)
  "config": {
    "1": {
      "name": "key",
      "label": "Input Name",
      "value": 10
    }
  }
```



![example_farmware_form.png](/images/example_farmware_form.png)

Input values are retrieved in a Farmware via `get_config_value`, as shown in this example:


__Using inputs:__

```python
from farmware_tools import get_config_value

VALUE = get_config_value('Farmware Name', 'key')

# or
# VALUE = get_config_value(farmware_name='Farmware Name', config_name='key', value_type=int)
```

__legacy:__

```python
import os

VALUE = os.environ['farmware_name_key']
```

The default value in `config` is provided if no change has been made to the Web App Farmware input form.

The default input value type is `int` (integer). For string input, use a `value_type` of `str`.

See [Hello Farmware Input](https://github.com/FarmBot-Labs/hello-farmware-input) for a complete working example.

# Currently supported languages and packages

 * __Python 3.7__: opencv, numpy, requests, serial, farmware_tools

__Python 3:__
FarmBot OS (v7+) now uses Python 3. Python 2 is no longer supported.



# Farmware manifest

To [install a Farmware](#section-installing-farmware), you need to create a `manifest.json` file and host it. The manifest URL will be the URL used when installing the Farmware.

For example, entering `https://raw.githubusercontent.com/FarmBot-Labs/hello-farmware/master/manifest.json` and clicking install on the Farmware page of the Web App would install the `Hello Farmware` Farmware, whose source code is located at the GitHub project [here](https://github.com/FarmBot-Labs/hello-farmware).


__Farmware Manifest Example (v7):__

```json

 "package": "Hello Farmware",
 "language": "python",
 "author": "FarmBot, Inc.",
 "description": "A simple Farmware example that tells FarmBot to log a new message.",
 "version": "1.0.0",
 "min_os_version_major": 6,
 "url": "https://raw.githubusercontent.com/FarmBot-Labs/hello-farmware/master/manifest.json",
 "zip": "https://github.com/FarmBot-Labs/hello-farmware/archive/master.zip",
 "executable": "python",
 "args": ["hello-farmware-master/hello.py"]
```

__v8:__

```json

 "package": "Hello Farmware",
 "language": "python",
 "author": "FarmBot, Inc.",
 "description": "A simple Farmware example that tells FarmBot to log a new message.",
 "farmware_manifest_version": "2.0.0",
 "package_version": "1.0.0",
 "farmbot_os_version_requirement": "> 7.0.1",
 "url": "https://raw.githubusercontent.com/FarmBot-Labs/hello-farmware/master/manifest.json",
 "zip": "https://github.com/FarmBot-Labs/hello-farmware/archive/master.zip",
 "executable": "python",
 "args": "hello-farmware-master/hello.py"
}
```

__v7 -> v8:__

```json
Instructions for migrating Farmware manifests from FarmBot OS v7 to FarmBot OS v8:
* Add `"farmware_manifest_version": "2.0.0",`.
* Rename `version` to `package_version`.
* Remove brackets from `args` value (for example, change `"args": ["run.py"]` to `"args": "run.py"`) and convert to string if necessary (`"run.py arg"`).
* Change `"min_os_version_major": 6,` to `"farmbot_os_version_requirement": ">= 8.0.0-any",`.
* If it exists, change `config` field from an array to an object where the key is the config input order (for example, change `"config": [{"name": "config_name", "label": "config label", "value": "default value"}]` to `"config": {"0": {"name": "config_name", "label": "config label", "value": "default value"}}`).
* If it exists, remove `farmware_tools_version`.
```

`zip` points to the hosted source code zip file. Github makes this easy: just add `/archive/master.zip` to the end of the GitHub repository URL, and insert `<repository name>-master/` to the beginning of the script filename to run, as seen in the manifest example above.

A Farmware manifest must be valid JSON and can be checked by any JSON parser or validator.

For additional manifest hosting methods, see [Workflows](doc:workflows).

# More about Farmware Tools

As shown in the examples on this page, a `farmware_tools` package **comes pre-installed on FarmBot OS** for ease of Farmware development.

## Local Farmware development

To view a list of available commands, install `farmware_tools` on your computer,
```bash
pip install --user farmware_tools
```

and open a Python console (run `python` in a terminal window).
In the Python console, type:
```python
import farmware_tools
help(farmware_tools.device)
```
Also see `help(farmware_tools.app)` and `help(farmware_tools.get_config_value)`

An [HTML interface](https://www.pydoc.io/pypi/farmware-tools-1.0.0) of the function list is also available, but may be missing some information.

### Install a specific version

While the latest version of `farmware_tools` is available for import in any Farmware when executed on FarmBot OS, you can install a specific version by specifying the version in the Farmware manifest:


__Optional version specification (v7):__

```json

  "package": "Farmware Name",
  // Other fields omitted for clarity (see the `Farmware manifest` section)
  "farmware_tools_version": "v3.0.0",
```

__v8:__

```json

  "package": "Farmware Name",
  // Other fields omitted for clarity (see the `Farmware manifest` section)
  "farmware_tools_version_requirement": ">= 3.3.0",
```

For local development you can install a specific version via `pip install --user farmware_tools==3.3.0`. Use `pip install --user --upgrade farmware_tools` to upgrade.
