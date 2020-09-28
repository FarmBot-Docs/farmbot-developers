---
title: "Farmware Hosting and Workflows"
slug: "farmware-hosting-and-workflows"
excerpt: "Farmware hosting options"
---

* toc
{:toc}

A Farmware generally includes Python code that is run by FarmBot OS. During development, you may first write and run the Python code on your local computer. To run it with FarmBot OS, the code must be hosted on a server from which FarmBot OS can download it.

All of the following methods require a minimum of two files:
* __A Farmware manifest__: `manifest.json`. (see the [Farmware manifest](farmware#farmware-manifest) for general info)
* __The Farmware code__: a `.py` file that contains or runs the code you've written. (See [Farmware](../farmware.md).)

For example Farmware files, see [Hello Farmware](https://github.com/FarmBot-Labs/hello-farmware).

{%
include callout.html
type="info"
title="Farmware code filenames"
content="The following examples use `my_farmware_code.py`, but a different name should be chosen for your main Farmware code file."
%}

Farmware is downloaded by FarmBot OS by installing it via the Web App FarmBot OS is connected to, which can either be self-hosted or at the public [my.farm.bot](https://my.farm.bot/). The `manifest.json` file URL is used for installation. See [Installing Farmware](https://software.farm.bot/v6/docs/farmware#installing-farmware) in the user documentation for basic UI operation.

Farmware can be run via the Web App by selecting it on the Farmware page and pressing <span class="fb-button fb-green">run</span>. (See [Farmware](https://software.farm.bot/v6/docs/farmware#farmware) in the user documentation for basic UI operation.)

Troubleshooting tips can be found on the [Common Farmware Problems](common-farmware-problems.md) page.

A typical heavy development workflow might include all of the following options in order. If a Linux system is not available, one might skip options 2 and 3 (which require running a server or building FarmBot OS). If Python is not available, one might skip options 1-3 and write a Farmware directly on GitHub. Published Farmware are usually hosted in a GitHub repository.

For the examples below, you can assume you want your Farmware to tell your FarmBot to say "Hi!" and so `my_farmware_code.py` contains the following code:
```python
from farmware_tools import device
device.log('Hi!')
```

# Option 1: Python (without FarmBot OS)

|                              |                              |
|------------------------------|------------------------------|
|**Description**               |Run the Python code on your computer
|**Pros**                      |Fastest updates<br>Most robust debugging for the code itself
|**Cons**                      |Does not reflect the FarmBot OS environment where the code will eventually be run

Step 1. Write some Python code.

Step 2. Run it via Python.

{%
include callout.html
type="info"
title="Using farmware_tools on your computer"
content="To run code that imports `farmware_tools` on your computer (without FarmBot OS), you will need to install the package via `pip install --user farmware_tools`. FarmBot OS already has the package built in."
%}

# Option 2: Localhost (run FarmBot OS locally)

|                              |                              |
|------------------------------|------------------------------|
|**Description**               |Run FarmBot OS on your computer.
|**Pros**                      |Allows direct editing of Farmware code
|**Cons**                      |Must be able to compile FarmBot OS on a compatible system. (see [FarmBot OS](../farmbot-os.md))



{%
include callout.html
type="warning"
title=""
content="This option is not recommended unless you are familiar with Linux and building Elixir apps."
%}

Step 1. Follow the instructions for setting up a local development environment for [FarmBot OS](../farmbot-os.md).

Step 2. Create a Farmware manifest and zip file containing your Python code and start an HTTP server on your computer. (e.g., `python3 -m http.server 8000 --bind 127.0.0.1`). Alternatively, use one of the other hosting methods.


__manifest.json (FBOS v8+):__

```json

 "package": "my-farmware",
 "language": "python",
 "author": "me",
 "description": "A description of my Farmware.",
 "farmware_manifest_version": "2.0.0",
 "package_version": "1.0.0",
 "farmbot_os_version_requirement": ">= 8.0.0",
 "url": "http://127.0.0.1:8000/manifest.json",
 "zip": "http://127.0.0.1:8000/zipped_farmware.zip",
 "executable": "python",
 "args": "my_farmware_code.py"
```

Step 3. Install the Farmware via the `manifest.json` file url at the HTTP server address. (e.g., `http://127.0.0.1:8000/manifest.json` if using the locally hosted method)

Step 4. Open the Farmware code (e.g., `my_farmware_code.py`) in the FarmBot OS `farmbot_os/tmp/farmware` directory.

Step 5. Edit the Farmware. Once changes are saved, running the Farmware will run the updated version.

# Option 3: HTTP server host method

|                              |                              |
|------------------------------|------------------------------|
|**Description**               |Host the Farmware from your own server
|**Pros**                      |Faster updates
|**Cons**                      |More involved process<br>Limited hosting availability

Step 1. Create a Farmware manifest and zip file containing your Python code.


__manifest.json (FBOS v8+):__

```json

 "package": "my-farmware",
 "language": "python",
 "author": "me",
 "description": "A description of my Farmware.",
 "farmware_manifest_version": "2.0.0",
 "package_version": "1.0.0",
 "farmbot_os_version_requirement": ">= 8.0.0",
 "url": "http://192.168.0.100:8000/manifest.json",
 "zip": "http://192.168.0.100:8000/zipped_farmware.zip",
 "executable": "python",
 "args": "my_farmware_code.py"
```

(where `192.168.0.100` is the IP address of your computer running the file server and `zipped_farmware.zip` is the name of the zip file containing `my_farmware_code.py`)

Step 2. Start an HTTP server on your computer. (e.g., `python3 -m http.server 8000`)

Step 3. Install the Farmware via the `manifest.json` file url at the HTTP server address. (e.g., `http://192.168.0.100:8000/manifest.json`, where `192.168.0.100` is the IP address of your computer running the file server.)

Step 4. After editing the Farmware, the code must be re-zipped and the Farmware either re-installed or updated by bumping the `version` value in `manifest.json` and pressing the UPDATE button in the Web App.

# Option 4: GitHub host methods

|                              |                              |
|------------------------------|------------------------------|
|**Description**               |Host Farmware code on GitHub for download and running by FarmBot OS installed on a Raspberry Pi
|**Pros**                      |Easy hosting<br>The `.zip` file is created automatically
|**Cons**                      |Updates to served files can be slow

Step 1. Create a new GitHub repository or Gist.

Step 2. Add a `manifest.json` file.


__manifest.json (GitHub, FBOS v8+):__

```json

 "package": "my-farmware",
 "language": "python",
 "author": "me",
 "description": "A description of my Farmware.",
 "farmware_manifest_version": "2.0.0",
 "package_version": "1.0.0",
 "farmbot_os_version_requirement": ">= 8.0.0",
 "url": "https://raw.githubusercontent.com/gh_username/repo-name/master/manifest.json",
 "zip": "https://github.com/gh_username/repo-name/archive/master.zip",
 "executable": "python",
 "args": "repo-name-master/my_farmware_code.py"
```

(where `gh_username` is your GitHub username and `repo-name` is the GitHub repository name) See [Farmware](../farmware.md#farmware-manifest) for a real-world example.


__manifest.json (Gist, FBOS v8+):__

```json

 "package": "my-farmware",
 "language": "python",
 "author": "me",
 "description": "A description of my Farmware.",
 "farmware_manifest_version": "2.0.0",
 "package_version": "1.0.0",
 "farmbot_os_version_requirement": ">= 8.0.0",
 "url": "",
 "zip": "https://gist.github.com/gh_username/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx/archive/master.zip",
 "executable": "python",
 "args": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx-master/my_farmware_code.py"
```

(where `xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx` is the Gist ID found in the URL)

Step 3. Install via the raw `manifest.json` file url and run.

Step 4. After editing the Farmware,
  * if using GitHub, it can be updated by bumping the `version` value in `manifest.json` and pressing the UPDATE button in the Web App.
  * if using Gist, the Farmware must be uninstalled and re-installed. (Bumping the version is not necessary when using Gist).
