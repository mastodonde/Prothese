# Python BLE GATT Server (peripheral)
GATT is constructed out of one or more server devices (BLE peripherals) and a client device (BLE central).

A GATT server is usually a small device such as a sensor, but for some use cases you might want to have a Linux computer such as a RPi used as a GATT server. This example is meant to demonstrate how this can be done.


## Setup
The instructions in this document were tested on Ubuntu 16.04.

## myo_read_raw Installation
This module requires myo_read_raw to be installed. View installation details :
https://github.com/ClubSynapsETS/Prothese/tree/master/Software/comm/Myo_read_raw

### Bluez Installation
On most distributions, you will need to upgrade Bluez in order to make this work.

Install dependencies:
```bash
sudo apt-get update
sudo apt-get install libudev-dev libical-dev libreadline-dev libglib2.0-dev libdbus-1-dev
```

Download and install Bluez

```bash
wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.45.tar.xz
tar xvf bluez-5.45.tar.xz
cd bluez-5.45/
./configure
make
sudo make install
```

Enable experimental features for the bluetooth driver: 
- `sudo nano /lib/systemd/system/bluetooth.service`
- Add `--experimental` to `ExecStart`. The line should look like this: 

    `ExecStart=/usr/local/libexec/bluetooth/bluetoothd --experimental`

Reload the service:
```bash
systemctl daemon-reload
sudo service bluetooth restart
```

## Usage
```bash
pip3 install -e micro_comm
python3 gatt_server_example.py
```

You can use a smartphone as a GATT client. I used the [GATT-IP](http://www.gatt-ip.org/) app, here it is on the [Google Play Store](https://play.google.com/store/apps/details?id=org.gatt_ip.activity&hl=en) and on the [App Store](https://itunes.apple.com/us/app/gatt-ip-bluetooth-smart-le-proxy-protocol/id940105344?mt=8)

![](http://jumper-public.s3-website.eu-central-1.amazonaws.com/gatt-ip.gif)

## License
The code in this repository is based on code taken from the [BlueZ](http://www.bluez.org/) project. It is licensed under GPL 2.0
