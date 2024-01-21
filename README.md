# Anthem Serial for Home Assistant

Custom Anthem Serial component written in Python3 for Home Assistant. Controls older, serial based, [Anthem] <abbr title="Audio & video">A/V</abbr> receivers and processors. Newer, IP based, receivers are controlled with [Anthem AV](https://www.home-assistant.io/integrations/anthemav/) plugin.

## Supported features

- turn on/off
- set input
- volume control

RS-232 control [codes](https://www.anthemav.com/downloads/anthemMRX_RS-232.071811.zip) are used as a reference.

## Supported models

- [MRX 700](https://www.anthemav.com/products-archived/model=mrx-700/page=overview)

[Anthem]: https://www.anthemav.com/

## Installation

1. Copy the custom_components folder to your own hassio /config folder.

2. A serial port is needed. When using a USB to serial dongle, it is recommeneded to use a udev rule, following this [tutorial](https://hackaday.io/project/183711-mks-tft28-with-klipper/log/202591-udev-rules). The USB port path as unique identifier is unique. In `/etc/udev/rules.d/98-local.rules`, add for instance:
```
ENV{ID_BUS}=="usb", ENV{ID_PATH_TAG}=="platform-3f980000_usb-usb-0_1_2_6_1_0", SYMLINK+="ampli"
```

A `/dev/ampli` link is created by udev. Then the home assistant device section, add:

```yaml
- name: avr
  platform: anthem_serial
  port: /dev/ampli
```

A `media_player.avr` object will be available for configuration.
