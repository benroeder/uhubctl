uhubctl
=======

`uhubctl` is utility to control USB power per-port on smart USB hubs.
Smart hub is defined as one that implements per-port power switching.

Original idea for this code was inspired by hub-ctrl.c by Niibe Yutaka:
https://www.gniibe.org/development/ac-power-control-by-USB-hub


Compatible USB hubs
===================

Note that not many USB hubs correctly support per-port power switching.
Some of them are no longer manufactured and can be hard to find.

This is list of known compatible USB hubs:

| Manufacturer       | Product                                              | Ports | USB | VID:PID   | Release | EOL  |
|:-------------------|:-----------------------------------------------------|:------|:----|:----------|:--------|:-----|
| Acer               | BE270U monitor ([see](https://tinyurl.com/acer550))  | 4     | 3.0 |`2109:2811`| 2016    |      |
| AmazonBasics       | HU3641V1 ([RPi issue](https://goo.gl/CLt46M))        | 4     | 3.0 |`2109:2811`| 2013    |      |
| AmazonBasics       | HU3770V1 ([RPi issue](https://goo.gl/CLt46M))        | 7     | 3.0 |`2109:2811`| 2013    |      |
| AmazonBasics       | HU9003V1EBL, HUC9003V1EBL                            | 7     | 3.1 |`2109:2817`| 2018    |      |
| AmazonBasics       | HU9002V1SBL, HU9002V1EBL, HU9002V1ESL ([note](https://tinyurl.com/HU9002)) | 10    | 3.1 |`2109:2817`| 2018    |      |
| AmazonBasics       | HUC9002V1SBL, HUC9002V1EBL, HUC9002V1ESL             | 10    | 3.1 |`2109:2817`| 2018    |      |
| AmazonBasics       | U3-7HUB (only works for 1 charge port)               | 7     | 3.0 |`2109:2813`| 2020    |      |
| Anker              | AK-68ANHUB-BV7A-0004 ([note](https://git.io/JLnZb))  | 7     | 3.0 |`2109:0812`| 2014    |      |
| Apple              | Mac Mini M4 (2 front ports only)                     | 2     | 3.2 |`05AC:800B`| 2024    |      |
| Apple              | Pro Display XDR MWPE2LL/A (internal USB hub)         | 4     | 2.0 |`05AC:9139`| 2019    |      |
| Apple              | Thunderbolt Display 27" (internal USB hub)           | 6     | 2.0 |           | 2011    | 2016 |
| Apple              | USB Keyboard With Numeric Pad (internal USB hub)     | 3     | 2.0 |           | 2011    |      |
| Asus               | Z77 Sabertooth Motherboard (onboard USB hub)         | 6     | 2.0 |           | 2012    |      |
| Asus               | Z87-PLUS Motherboard (onboard USB hub)               | 4     | 3.0 |           | 2013    | 2016 |
| Aukey              | CB-C59                                               | 4     | 3.0 |`2109:2813`| 2017    |      |
| B+B SmartWorx      | UHR204                                               | 4     | 2.0 |`0856:DB00`| 2013    |      |
| B+B SmartWorx      | USH304                                               | 4     | 3.0 |`04B4:6506`| 2017    | 2019 |
| Basler             | 2000036234                                           | 4     | 3.0 |`0451:8046`| 2016    |      |
| Belkin             | F5U101                                               | 4     | 2.0 |`0451:2046`| 2005    | 2010 |
| Belkin             | F5U238UKCRL-MOB                                      | 4     | 2.0 |`0409:0059`| 2004    | 2010 |
| BenQ               | PD2700U 4K Monitor (works only in USB2 mode)         | 4     | 3.0 |`05E3:0610`| 2018    |      |
| BenQ               | PD3220U                                              | 4     | 3.1 |`05E3:0610`| 2019    |      |
| Bytecc             | BT-UH340 ([warning](https://tinyurl.com/BT-UH340-1)) | 4     | 3.0 |`2109:8110`| 2010    |      |
| Centech            | CT-USB4HUB ReTRY HUB                                 | 4     | 3.0 |`0424:2744`| 2017    |      |
| Circuitco          | Beagleboard-xM (internal USB hub)                    | 4     | 2.0 |`0424:9514`| 2010    |      |
| Club3D             | CSV-3242HD Dual Display Docking Station              | 4     | 3.0 |`2109:2811`| 2015    |      |
| Coolgear           | USBG-12U2ML                                          | 12    | 2.0 |`05e3:0607`| 2015    |      |
| Cypress            | CY4608 HX2VL ([note](https://tinyurl.com/CY4608-1))  | 4     | 2.0 |`04B4:6570`| 2012    |      |
| D-Link             | DUB-H4 rev D,E (black). Note: rev A,C,F not supported| 4     | 2.0 |`05E3:0608`| 2012    |      |
| D-Link             | DUB-H7 rev A (silver)                                | 7     | 2.0 |`2001:F103`| 2005    | 2010 |
| D-Link             | DUB-H7 rev D,E (black). Rev B,C,F,G not supported    | 7     | 2.0 |`05E3:0608`| 2012    |      |
| Dell               | P2416D 24" QHD Monitor ([note](https://git.io/JUAu8))| 4     | 2.0 |           | 2017    |      |
| Dell               | S2719DGF 27" WQHD Gaming-Monitor                     | 5     | 3.0 |`0424:5734`| 2018    |      |
| Dell               | UltraSharp 1704FPT 17" LCD Monitor                   | 4     | 2.0 |`0424:A700`| 2005    | 2015 |
| Dell               | UltraSharp U2415 24" LCD Monitor                     | 5     | 3.0 |           | 2014    |      |
| Dell               | UltraSharp U3419W 34" Curved Monitor                 | 6     | 3.0 |           | 2020    |      |
| Dell               | Wyse 3040 ([-f required](https://tinyurl.com/wyse3k))| 6     | 3.0 |           | 2017    |      |
| Delock             | 62537                                                | 4     | 3.0 |           | 2017    | 2021 |
| Delock             | 87445 ([note](https://git.io/Jsuz5))                 | 4     | 2.0 |`05E3:0608`| 2009    | 2013 |
| Elecom             | U2H-G4S                                              | 4     | 2.0 |           | 2006    | 2011 |
| Gigabyte           | G27Q monitor ([see](http://tinyurl.com/G27Q551))     | 4     | 3.0 |`2109:0817`| 2020    |      |
| GlobalScale        | ESPRESSObin SBUD102 V5                               | 1     | 3.0 |`1D6B:0003`| 2017    |      |
| Hardkernel         | ODROID-C4 ([note](https://git.io/JG0mP))             | 4     | 3.0 |           | 2020    |      |
| Hawking Technology | UH214                                                | 4     | 2.0 |           | 2003    | 2008 |
| Hewlett Packard    | USB-C Dock G5 5TW10AA                                | 5     | 3.0 |`03F0:076B`| 2019    |      |
| Hewlett Packard    | P5Q58UT                                              | 3     | 3.0 |           | 2019    |      |
| Inateck            | HB2025A ([USB2 only](https://tinyurl.com/HB2025A-1)) | 4     | 3.1 |`2109:2822`| 2021    |      |
| IOI                | U3H415E1                                             | 4     | 3.0 |           | 2012    |      |
| j5create           | JUH377 ([note](https://tinyurl.com/JUH377))          | 7     | 3.0 |           | 2016    |      |
| j5create           | JUH470 ([note](https://tinyurl.com/JUH470))          | 3     | 3.0 |`05E3:0610`| 2014    |      |
| Juiced Systems     | 6HUB-01                                              | 7     | 3.0 |`0BDA:0411`| 2014    | 2018 |
| KUNBUS GmbH        | RevPi Connect (+) / S / SE                           | 2     | 2.0 |`0424:9514`| 2018    |      |
| KUNBUS GmbH        | RevPi Connect 4                                      | 2     | 3.0 |           | 2022    |      |
| KUNBUS GmbH        | RevPi Core 3 / S / SE                                | 2     | 2.0 |`0424:9514`| 2017    |      |
| LG Electronics     | 27MD5KL-B monitor                                    | 4     | 3.0 |`043E:9A60`| 2019    |      |
| LG Electronics     | 27GL850-B monitor                                    | 4     | 3.0 |`0451:8142`| 2019    |      |
| LG Electronics     | 27UK850-W monitor                                    | 2     | 3.0 |           | 2018    |      |
| LG Electronics     | 27UN83A-W monitor                                    | 2     | 3.0 |`0451:8142`| 2020    |      |
| LG Electronics     | 38WK95C-W monitor                                    | 4     | 3.0 |`0451:8142`| 2018    |      |
| Lenovo             | ThinkPad Ultra Docking Station (40A20090EU)          | 6     | 2.0 |`17EF:100F`| 2015    |      |
| Lenovo             | ThinkPad Ultra Docking Station (40AJ0135EU)          | 7     | 3.1 |`17EF:3070`| 2018    |      |
| Lenovo             | ThinkPad X200 Ultrabase 42X4963                      | 3     | 2.0 |`17EF:1005`| 2008    | 2011 |
| Lenovo             | ThinkPad X6 Ultrabase 42W3107                        | 4     | 2.0 |`17EF:1000`| 2006    | 2009 |
| Lenovo             | ThinkPlus 4-in-1 USB-C hub 4X90W86497                | 3     | 3.0 |           | 2021    |      |
| Lenovo             | ThinkVision T24i-10 Monitor                          | 4     | 2.0 |`17EF:0610`| 2018    |      |
| Lenovo             | USB-C to 4 Port USB-A Hub ([USB2 only](https://github.com/mvp/uhubctl/issues/625)) | 4     | 2.0 |`17EF:103A`| 2020    |      |
| Lindy              | USB serial converter 4 port                          | 4     | 1.1 |`058F:9254`| 2008    |      |
| Linksys            | USB2HUB4 ([note](https://git.io/JYiDZ))              | 4     | 2.0 |           | 2004    | 2010 |
| Maplin             | A08CQ                                                | 7     | 2.0 |`0409:0059`| 2008    | 2011 |
| Metadot            | Das Keyboard 4                                       | 2     | 3.0 |           | 2014    |      |
| Microchip          | EVB9512                                              | 2     | 2.0 |           | 2009    |      |
| Microchip          | EVB-USB2517                                          | 7     | 2.0 |           | 2008    |      |
| Microchip          | EVB-USB2534BC                                        | 4     | 2.0 |           | 2013    |      |
| Microchip          | EVB-USB5807                                          | 7     | 3.0 |           | 2016    |      |
| Moxa               | Uport-407                                            | 7     | 2.0 |`110A:0407`| 2009    |      |
| NVidia             | Jetson Nano B01 ([details](https://git.io/JJaFR))    | 4     | 3.0 |           | 2019    |      |
| NVidia             | Jetson Xavier NX ([details](https://tinyurl.com/Xavier-NX)) | 4     | 3.0 |           | 2020    |      |
| Phidgets           | HUB0003_0                                            | 7     | 2.0 |`1A40:0201`| 2017    |      |
| Philips            | 346B1C UltraWide 34" Curved Monitor                  | 4     | 3.0 |`05E3:0610`| 2019    |      |
| Plugable           | USB3-HUB7BC                                          | 7     | 3.0 |`2109:0813`| 2015    |      |
| Plugable           | USB3-HUB7C (only works for 2 charge ports)           | 7     | 3.0 |`2109:0813`| 2015    |      |
| Plugable           | USBC-HUB7BC (works for 6/7 ports, not the rightmost) | 7     | 3.0 |`2109:0817`| 2021    |      |
| Plugable           | USB3-HUB10-C2 (only works for 2 charge ports)        | 10    | 3.0 |           | 2014    |      |
| Port Inc           | NWUSB01                                              | 4     | 1.1 |`0451:1446`| 1999    | 2003 |
| Raspberry Pi       | B+, 2B, 3B ([see below](#raspberry-pi-b2b3b))        | 4     | 2.0 |           | 2011    |      |
| Raspberry Pi       | 3B+        ([see below](#raspberry-pi-3b))           | 4     | 2.0 |`0424:2514`| 2018    |      |
| Raspberry Pi       | 4B         ([see below](#raspberry-pi-4b))           | 4     | 3.0 |`2109:3431`| 2019    |      |
| Raspberry Pi       | 5          ([see below](#raspberry-pi-5))            | 4     | 3.0 |`1d6b:0002`| 2023    |      |
| Renesas            | uPD720202 PCIe USB 3.0 host controller               | 2     | 3.0 |           | 2013    |      |
| Rosewill           | RHUB-210                                             | 4     | 2.0 |`0409:005A`| 2011    | 2014 |
| Rosonway           | RSH-518C ([note](https://tinyurl.com/RSH518))        | 7     | 3.0 |`2109:0817`| 2021    |      |
| Rosonway           | RSH-A10 ([see](https://tinyurl.com/2ppyyaj8))        | 10    | 3.0 |`0bda:0411`| 2020    |      |
| Rosonway           | RSH-A13 ([warning](https://tinyurl.com/RSH-A13))     | 13    | 3.1 |`2109:2822`| 2021    |      |
| Rosonway           | RSH-A16 ([note](https://git.io/JTawg), [warning](https://tinyurl.com/RSH-A16)) | 16    | 3.0 |`0bda:0411`| 2020    |      |
| Rosonway           | RSH-A37S                                             | 7     | 3.0 |`2109:2822`| 2021    |      |
| Rosonway           | RSH-A104 ([USB2 only](https://tinyurl.com/RSH-A104)) | 4     | 3.1 |`2109:2822`| 2022    |      |
| Rosonway           | RSH-ST07C ([only 4](https://tinyurl.com/4pjnujrn))   | 7     | 3.0 |`2109:2822`| 2023    |      |
| Rosonway           | RSH-ST10C-6 ([note](https://tinyurl.com/428vpa2f))   | 10    | 3.1 |           | 2024    |      |
| Sanwa Supply       | USB-HUB14GPH                                         | 4     | 1.1 |           | 2001    | 2003 |
| Seagate            | Backup Plus Hub STEL8000100                          | 2     | 3.0 |`0BC2:AB44`| 2016    |      |
| Seeed Studio       | reTerminal CM4104032                                 | 2     | 2.0 |`0424:2514`| 2021    |      |
| StarTech           | DKT30CSDHPD3 USB-C Travel Dock                       | 3     | 3.0 |`2109:2817`| 2018    |      |
| StarTech           | HB30A4AIB ([warning](https://tinyurl.com/ycxravwk))  | 4     | 3.0 |`2109:2817`| 2018    |      |
| StarTech           | HB31C2A2CB ([note](https://github.com/mvp/uhubctl/issues/601)) | 5 | 3.0 |`14B0:013D`| 2020    |      |
| Sunix              | SHB4200MA                                            | 4     | 2.0 |`0409:0058`| 2006    | 2009 |
| System Talks       | Sugoi USB2-HUB4X                                     | 4     | 2.0 |           | 2007    |      |
| Targus             | ACH155 (port 3 controls all ports)                   | 4     | 3.0 |           | 2022    |      |
| Targus             | PA095UZ                                              | 2     | 2.0 |           | 2004    |      |
| Targus             | PAUH212/PAUH212U                                     | 7     | 2.0 |           | 2004    | 2009 |
| Texas Instruments  | TUSB4041PAPEVM                                       | 4     | 2.1 |`0451:8142`| 2015    |      |
| UUGear             | MEGA4 (for Raspberry Pi 4B)                          | 4     | 3.0 |`2109:0817`| 2021    |      |
| VirtualHere        | USB3 4-port hub ([note](https://tinyurl.com/vhusb))  | 4     | 3.0 |           | 2024    |      |

This table is by no means complete.
If your hub works with `uhubctl`, but is not listed above, please report it
by opening new issue at https://github.com/mvp/uhubctl/issues,
so we can add it to supported table. In your report, please provide
exact product model and add output from `uhubctl`
and please test VBUS off support as described below in FAQ.

Note that quite a few modern motherboards have built-in root hubs that
do support this feature - you may not even need to buy any external hub.


USB 3.0 duality note
====================
If you have USB 3.0 hub connected to USB3 upstream port, it will be detected
as 2 independent virtual hubs: USB2 and USB3, and your USB devices will be connected
to USB2 or USB3 virtual hub depending on their capabilities and connection speed.
To control power for such hubs, it is necessary to turn off/on power on **both** USB2 and USB3
virtual hubs for power off/on changes to take effect. `uhubctl` will try to do this automatically
(unless you disable this behavior with option `-e`).

Unfortunately, while most hubs will cut off data USB connection, some may still not cut off VBUS to port,
which means connected phone may still continue to charge from port that is powered off by `uhubctl`.

Installing
==========

For Linux and MacOS uhubctl is available in standard package managers
and can be installed with following commands:

* MacOS: `brew install uhubctl` or `sudo port install uhubctl`
* Ubuntu/Debian/Raspbian: `sudo apt install uhubctl`
* Redhat/EPEL/Fedora/CentOS: `sudo yum install uhubctl`
* OpenSUSE: `sudo zypper install uhubctl`

However, uhubctl installed from standard package manager may not
necessarily be latest version, or even severely lag behind current version.
If [latest published](https://github.com/mvp/uhubctl/releases) uhubctl version
is newer than what your package manager offers, you may need to compile and install
from source as described below.

Compiling
=========

This utility was tested to compile and work on Linux (Ubuntu/Debian/Raspbian,
Redhat/EPEL/Fedora/CentOS, Arch Linux, Gentoo, openSUSE, Buildroot),
FreeBSD, NetBSD, SunOS and MacOS.

While `uhubctl` compiles on Windows, USB power switching does not work on Windows because `libusb`
is using `winusb.sys` driver, which according to Microsoft does not support
[necessary USB control requests](https://web.archive.org/web/20210225235523/https://social.msdn.microsoft.com/Forums/sqlserver/en-US/f680b63f-ca4f-4e52-baa9-9e64f8eee101/how-to-send-an-quotusb-control-requestquot-to-an-usbhub?forum=wdk).
This may be fixed if `libusb` starts supporting different driver on Windows.

Note that it is highly recommended to have utility `pkgconf` (or `pkg-config`) installed
(often it is installed by default).

First, you need to install library libusb-1.0 (version 1.0.13 or later is required,
1.0.23 or later is recommended):

* Ubuntu: `sudo apt-get install libusb-1.0-0-dev pkgconf`
* Redhat: `sudo yum install libusb1-devel pkgconf`
* OpenSUSE: `sudo zypper install libusb-1_0-devel pkgconf`
* MacOS: `brew install libusb pkgconf`, or `sudo port install libusb-devel pkgconf`
* FreeBSD: `pkg install gmake pkgconf` (libusb is included by default)
* NetBSD: `sudo pkgin install libusb1 gmake pkgconf`
* Windows: TBD?

To fetch uhubctl source and compile it:

    git clone https://github.com/mvp/uhubctl
    cd uhubctl
    make

This should generate `uhubctl` binary.
You can install it in your system as `/usr/sbin/uhubctl` using:

    sudo make install

Note that on some OS (e.g. FreeBSD/NetBSD) you need to use `gmake` instead to build.

Usage
=====

> :warning: On Linux, use `sudo` or configure USB permissions as described below!

To list all supported hubs:

    uhubctl

You can control the power on a USB port(s) like this:

    uhubctl -a off -p 2

This means operate on default smart hub and turn power off (`-a off`, or `-a 0`)
on port 2 (`-p 2`). Supported actions are `off`/`on`/`cycle`/`toggle` (or `0`/`1`/`2`/`3`).
`cycle` means turn power off, wait some delay (configurable with `-d`) and turn it back on.
Ports can be comma separated list, and may use `-` for ranges e.g. `2`, or `2,4`, or `2-5`, or `1-2,5-8`.

> :warning: Turning off built-in USB ports may cut off your keyboard or mouse,
so be careful which ports you are turning off!

If you have more than one smart USB hub connected, you should choose
specific hub to control using `-l` (location) parameter.
To find hub locations, simply run `uhubctl` without any parameters.
Hub locations look like `b-x.y.z`, where `b` is USB bus number, and `x`, `y`, `z`...
are port numbers for all hubs in chain, starting from root hub for a given USB bus.
This address is semi-stable - it will not change if you unplug/replug (or turn off/on)
USB device into the same physical USB port (this method is also used in Linux kernel).

To get the status in machine-readable JSON format, use `-j` option:

    uhubctl -j

This will output status of all hubs and ports in JSON format, making it easy to integrate
uhubctl with other tools and scripts. The JSON output includes all the same information
as the text output, including hub info, port status, connected devices, and their properties.


JSON Output
===========

The `-j` option enables JSON output for all commands, including status queries and power actions.
The JSON is pretty-printed with proper indentation for human readability.

Status Query JSON Format
------------------------

When querying hub status, the output follows this structure:

The `status` field provides three levels of detail:
- `raw`: Original hex value from USB hub
- `decoded`: Human-readable interpretation (e.g., "device_active", "powered_no_device")
- `bits`: Individual status bits broken down by name

```json
{
  "hubs": [
    {
      "location": "3-1.4",
      "description": "05e3:0610 GenesysLogic USB2.1 Hub, USB 2.10, 4 ports, ppps",
      "hub_info": {
        "vid": "0x05e3",
        "pid": "0x0610",
        "usb_version": "2.10",
        "nports": 4,
        "ppps": "ppps"
      },
      "ports": [
        {
          "port": 1,
          "status": {
            "raw": "0x0103",
            "decoded": "device_active",
            "bits": {
              "connection": true,
              "enabled": true,
              "powered": true,
              "suspended": false,
              "overcurrent": false,
              "reset": false,
              "highspeed": false,
              "lowspeed": false
            }
          },
          "flags": {
            "connection": true,
            "enable": true,
            "power": true
          },
          "human_readable": {
            "connection": "Device is connected",
            "enable": "Port is enabled",
            "power": "Port power is enabled"
          },
          "speed": "USB1.1 Full Speed 12Mbps",
          "speed_bps": 12000000,
          "vid": "0x0403",
          "pid": "0x6001",
          "vendor": "FTDI",
          "product": "FT232R USB UART",
          "device_class": 0,
          "class_name": "Composite Device",
          "usb_version": "2.00",
          "device_version": "6.00",
          "serial": "A10KZP45",
          "description": "0403:6001 FTDI FT232R USB UART A10KZP45"
        }
      ]
    }
  ]
}
```

Power Action JSON Events
------------------------

When performing power actions (on/off/toggle/cycle), uhubctl outputs real-time JSON events:

```bash
uhubctl -j -a cycle -l 3-1.4 -p 1 -d 2
```

Outputs events like:

```json
{"event": "hub_status", "hub": "3-1.4", "description": "05e3:0610 GenesysLogic USB2.1 Hub, USB 2.10, 4 ports, ppps"}
{"event": "power_change", "hub": "3-1.4", "port": 1, "action": "off", "from_state": true, "to_state": false, "success": true}
{"event": "delay", "reason": "power_cycle", "duration_seconds": 2.0}
{"event": "power_change", "hub": "3-1.4", "port": 1, "action": "on", "from_state": false, "to_state": true, "success": true}
```

Event types include:
- `hub_status`: Initial hub information
- `power_change`: Port power state change
- `delay`: Wait period during power cycling
- `hub_reset`: Hub reset operation (when using `-R`)

JSON Usage Examples
-------------------

Find all FTDI devices and show how to control them:
```bash
uhubctl -j | jq -r '.hubs[] | . as $hub | .ports[] | select(.vendor == "FTDI") | 
  "Device: \(.description)\nControl: uhubctl -l \($hub.location) -p \(.port) -a off\n"'
```

Find a device by serial number:
```bash
SERIAL="A10KZP45"
uhubctl -j | jq -r --arg serial "$SERIAL" '.hubs[] | . as $hub | .ports[] | 
  select(.serial == $serial) | "Found at hub \($hub.location) port \(.port)"'
```

List all empty ports:
```bash
uhubctl -j | jq -r '.hubs[] | . as $hub | .ports[] | 
  select(.vid == null) | "Empty: hub \($hub.location) port \(.port)"'
```

Generate CSV of all connected devices:
```bash
echo "Location,Port,VID,PID,Vendor,Product,Serial"
uhubctl -j | jq -r '.hubs[] | . as $hub | .ports[] | select(.vid) | 
  "\($hub.location),\(.port),\(.vid),\(.pid),\(.vendor // ""),\(.product // ""),\(.serial // "")"'
```

Monitor power action results:
```bash
uhubctl -j -a cycle -l 3-1 -p 2 | jq 'select(.event == "power_change")'
```


Linux USB permissions
=====================

On Linux, you should configure `udev` USB permissions (otherwise you will have to run it as root using `sudo uhubctl`).

Starting with Linux Kernel 6.0 there is a standard interface to turn USB hub ports on or off,
and `uhubctl` will try to use it (instead of `libusb`) to set the port status.
This is why there are additional rules for 6.0+ kernels.
There is no harm in having these rules on systems running older kernel versions.

To fix USB permissions, first run `sudo uhubctl` and note all `vid:pid` for hubs you need to control.
Then, add udev rules like below to file `/etc/udev/rules.d/52-usb.rules`
(replace `2001` with your hub vendor id, or completely remove `ATTR{idVendor}` filter to allow any USB hub access):

    SUBSYSTEM=="usb", DRIVER=="hub|usb", MODE="0666", ATTR{idVendor}=="2001"
    # Linux 6.0 or later (its ok to have this block present for older Linux kernels):
    SUBSYSTEM=="usb", DRIVER=="hub|usb", \
      RUN="/bin/sh -c \"chmod -f 666 $sys$devpath/*port*/disable || true\""

Note that for USB3 hubs, some hubs use different vendor ID for USB2 vs USB3 components of the same chip,
and both need permissions to make uhubctl work properly.
E.g. for Raspberry Pi 4B, you need to add these 2 lines (or remove idVendor filter):

    SUBSYSTEM=="usb", DRIVER=="hub|usb", MODE="0666", ATTR{idVendor}=="2109"
    SUBSYSTEM=="usb", DRIVER=="hub|usb", MODE="0666", ATTR{idVendor}=="1d6b"

If you don't like wide open mode `0666`, you can restrict access by group like this:

    SUBSYSTEM=="usb", DRIVER=="hub|usb", MODE="0664", GROUP="dialout"
    # Linux 6.0 or later (its ok to have this block present for older Linux kernels):
    SUBSYSTEM=="usb", DRIVER=="hub|usb", \
      RUN+="/bin/sh -c \"chown -f root:dialout $sys$devpath/*port*/disable || true\"" \
      RUN+="/bin/sh -c \"chmod -f 660 $sys$devpath/*port*/disable || true\""

and then add permitted users to `dialout` group:

    sudo usermod -a -G dialout $USER

For your `udev` rule changes to take effect, reboot or run:

    sudo udevadm trigger --attr-match=subsystem=usb

For your convenience, ready to use udev rule is provided [here](https://github.com/mvp/uhubctl/blob/master/udev/rules.d/52-usb.rules).


FAQ
===

#### _What is USB per-port power switching?_

According to USB 2.0 specification, USB hubs can advertise no power switching,
ganged (all ports at once) power switching or per-port (individual) power switching.
Note that by default `uhubctl` will only detect USB hubs which support per-port power switching
(but you can force it to try operating on unsupported hubs with option `-f`).
You can find what kind of power switching your hardware supports by using `sudo lsusb -v`:

No power switching:

    wHubCharacteristic 0x000a
      No power switching (usb 1.0)
      Per-port overcurrent protection

Ganged power switching:

    wHubCharacteristic 0x0008
      Ganged power switching
      Per-port overcurrent protection

Per-port power switching:

    wHubCharacteristic 0x0009
      Per-port power switching
      Per-port overcurrent protection


#### _How do I check if my USB hub is supported by `uhubctl`?_

1. Run `sudo uhubctl`. If your hub is not listed, it is not supported.
   Alternatively, you can run `sudo lsusb -v` and check for
   `Per-port power switching` -  if you cannot see such line in lsusb output,
   hub is not supported.
2. Check for VBUS (voltage) off support: plug a phone, USB light
    or USB fan into USB port of your hub.
   Try using `uhubctl` to turn power off on that port, and check
   that phone stops charging, USB light stops shining or USB fan stops spinning.
   If VBUS doesn't turn off, your hub manufacturer did not include circuitry
   to actually cut power off. Such hub would still work
   to cut off USB data connection, but it cannot turn off power,
   and we do not consider this supported device.
3. If tests above were successful, please report your hub
   by opening new issue at https://github.com/mvp/uhubctl/issues,
   so we can add it to list of supported devices.
   Please do not report unsupported hubs, unless it is different
   hardware revision of some already listed supported model.


#### _USB devices are not removed after port power down on Linux_

After powering down USB port, udev does not get any event, so it keeps the device files around.
However, trying to access the device files will lead to an IO error.

This is Linux kernel [issue](https://tinyurl.com/ym7yvuzw) and is [fixed](https://github.com/mvp/uhubctl/pull/450)
since uhubctl 2.5.0 for systems with Linux kernel 6.0 or later.

If you are still using Linux 5.x or older, you can use this workaround for this issue:

    sudo uhubctl -a off -l ${location} -p ${port}
    sudo udevadm trigger --action=remove /sys/bus/usb/devices/${location}.${port}/

Device file will be removed by udev, but USB device will be still visible in `lsusb`.
Note that path `/sys/bus/usb/devices/${location}.${port}` will only exist if device was detected on that port.
When you turn power back on, device should re-enumerate properly (no need to call `udevadm` again).

#### _Power comes back on after few seconds on Linux_

Some device drivers in kernel are surprised by USB device being turned off and automatically try to power it back on.

This is Linux kernel [issue](https://tinyurl.com/ym7yvuzw) and is [fixed](https://github.com/mvp/uhubctl/pull/450)
since uhubctl 2.5.0 for systems with Linux kernel 6.0 or later.

If you are still using Linux 5.x or older:

You can use option `-r N`, where N is some number from 10 to 1000 to fix this -
`uhubctl` will try to turn power off many times in quick succession, and it should suppress that.

Disabling USB authorization for device in question before turning power off with `uhubctl` should help:

    echo 0 > sudo tee /sys/bus/usb/devices/${location}.${port}/authorized

If your device is USB mass storage, invoking `udisksctl` before calling `uhubctl` should help too:

    sudo udisksctl power-off --block-device /dev/disk/...`
    sudo uhubctl -a off ...


#### _Multiple 4-port hubs are detected, but I only have one 7-port hub connected_

Many hub manufacturers build their USB hubs using basic 4 port USB chips.
E.g. to make 7 port hub, they daisy-chain two 4 port hubs - 1 port is lost to daisy-chaining,
so it makes it 4+4-1=7 port hub. Similarly, 10 port hub could be built as 3 4-port hubs
daisy-chained together, which gives 4+4+4-2=10 usable ports.

Note that you should never try to change power state for ports used to daisy-chain internal hubs together.
Doing so will confuse internal hub circuitry and will cause unpredictable behavior.


#### _Raspberry Pi turns power off on all ports, not just the one I specified_

This is the limitation of Raspberry Pi hardware design.
As a workaround, you can buy any external USB hub from supported list above,
attach it to any USB port of Raspberry Pi, and control power on its ports independently.
Also, there are supported hubs designed specifically for Raspberry Pi, e.g. UUGear MEGA4.

For reference, supported Raspberry Pi models have following internal USB topology:

##### Raspberry Pi B+,2B,3B

  * Single hub `1-1`, ports 2-5 ganged, all controlled by port `2`:

        uhubctl -l 1-1 -p 2 -a 0

    Trying to control ports `3`,`4`,`5` will not do anything.
    Port `1` controls power for Ethernet+WiFi.

##### Raspberry Pi 3B+

  * Main hub `1-1`, all 4 ports ganged, all controlled by port `2` (turns off secondary hub ports as well).
    Port `1` connects hub `1-1.1` below, ports `2` and `3` are wired outside, port `4` not wired.

        uhubctl -l 1-1 -p 2 -a 0

  * Secondary hub `1-1.1` (daisy-chained to main): 3 ports,
    port `1` is used for Ethernet+WiFi, and ports `2` and `3` are wired outside.


##### Raspberry Pi 4B

 > :warning: If your VL805 firmware is older than `00137ad` (check with `sudo rpi-eeprom-update`),
you have to [update firmware](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#rpi-eeprom-update)
to make power switching work on RPi 4B.

  * USB2 hub `1`, 1 port, only connects hub `1-1` below.

  * USB2 hub `1-1`, 4 ports ganged, dual to USB3 hub `2` below:

        uhubctl -l 1-1 -a 0

  * USB3 hub `2`, 4 ports ganged, dual to USB2 hub `1-1` above:

        uhubctl -l 2 -a 0

  * USB2 hub `3`, 1 port, OTG controller. Power switching is [not supported](https://git.io/JUc5Q).

##### Raspberry Pi 5

  Raspberry Pi 5 has two USB2 ports and two USB3 ports (total 4).
These ports are connected to 4 distinct USB hubs `1`,`2`,`3`,`4` in really weird configuration
(but depending on OS and HW revision hubs of interest can be `2`,`3`,`4`,`5`).
If USB3 device is connected to blue socket, it will be detected on USB3 hub `2` or `4`.
If USB2 device is connected to any socket or USB3 device connected to black socket,
it will be detected on USB2 hub `1` or `3`.
Regardless of USB2/USB3 connection type, blue sockets are always port `1`,
and black sockets are always port `2`.

  Each of 4 USB onboard hubs advertises as supporting per-port power switching, but this is not true.
In reality, Raspberry Pi 5 all 4 ports are ganged together in one group,
despite belonging to 4 different logical USB hubs.

To turn off VBUS power it has to be disabled across all onboard hubs and ports with:

   ```
   uhubctl -l 2 -a 0
   uhubctl -l 4 -a 0
   ```

To turn it back on:

   ```
   uhubctl -l 2 -a 1
   uhubctl -l 4 -a 1
   ```

Note that VBUS power goes down only if all ports are off -
enabling any single port enables VBUS back for all 4 ports.

Notable projects using uhubctl
==============================
| Project                                                  | Description                                             |
|:---------------------------------------------------------|:--------------------------------------------------------|
| [Morse code USB light](https://git.io/fj1F4)             | Flash a message in Morse code with USB light            |
| [Webcam USB light](https://git.io/fj1FB)                 | Turn on/off LED when webcam is turned on/off            |
| [Cinema Lightbox](https://goo.gl/fjCvkz)                 | Turn on/off Cinema Lightbox from iOS Home app           |
| [Build Status Light](https://goo.gl/3GA82o)              | Create a build status light in under 10 minutes         |
| [Buildenlights](https://git.io/fj1FC)                    | GitLab/GitHub project build status as green/red light   |
| [Weather Station](https://goo.gl/3b1FzC)                 | Reset Weather Station when it freezes                   |
| [sysmoQMOD](https://tinyurl.com/sysmoQMOD)               | Reset cellular modems when necessary                    |
| [Smog Sensor](https://tinyurl.com/smogsensor)            | Raspberry Pi based smog sensor power reset              |
| [Terrible Cluster](https://goo.gl/XjiXFu)                | Power on/off Raspberry Pi cluster nodes as needed       |
| [Ideal Music Server](https://tinyurl.com/ideal-m-srv)    | Turn off unused USB ports to improve audio quality      |
| [USB drives with no phantom load](https://goo.gl/qfrmGK) | Power USB drives only when needed to save power         |
| [USB drive data recovery](https://goo.gl/4MddLr)         | Recover data from failing USB hard drive                |
| [Control power to 3D printer](https://git.io/fh5Tr)      | OctoPrint web plugin for USB power control              |
| [USB fan for Raspberry Pi](https://tinyurl.com/fan-rpi)  | Control USB fan to avoid Raspberry Pi overheating       |
| [Raspberry Pi Reboot Router](https://tinyurl.com/rpi-rtr)| Automatically reboot router if internet isn't working   |
| [Control USB Lamp With Voice](https://tinyurl.com/usblmp)| Voice Control of USB Lamp using Siri and Raspberry Pi   |
| [Control USB LED Strip](https://tinyurl.com/usbleds)     | Controlling USB powered LED Light Strip                 |
| [Brew beer with Raspberry Pi](https://git.io/JtbLd)      | Automated beer brewing system using Raspberry Pi        |
| [Webcam On-Air Sign](https://tinyurl.com/uonair)         | Automatically light up a sign when webcam is in use     |
| [Do it yourself PPPS](https://git.io/J3lHs)              | Solder wires in your USB hub to support uhubctl         |
| [Open source PPPS hub](https://tinyurl.com/yckhystt)     | Open source hardware project for uhubctl compatible hub |
| [Python Wrapper for uhubctl](https://github.com/nbuchwitz/python3-uhubctl) | Module to use uhubctl with Python     |
| [labgrid](https://github.com/labgrid-project/labgrid)    | Framework for testing embedded Linux on hardware        |
| [Thermal Camera](https://tinyurl.com/5asne8hw)           | Turn on/off robot's thermal camera when necessary       |


Copyright
=========

Copyright (C) 2009-2025 Vadim Mikhailov

This file can be distributed under the terms and conditions of the
GNU General Public License version 2.
