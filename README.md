# airq
Air Quality

The project aims at building an air quality measurement station. The steps are mostly based on the [blog post](https://www.raspberrypi.org/blog/monitor-air-quality-with-a-raspberry-pi/), but shall be extended/modified in two respects:

* Explain the initial setup of a headless raspian on a new Raspberry Pi Zero W
* Store the information in Google Cloud

As a result a moderate technically interested person should be able to replicate the steps under supervision when having all hardware available.


## Raspberry Pi Zero W - Headless Setup
For making fast progress we will avoid connecting the Rasperry Pi with a keyboard and a monitor, but instead use a headless setup (headless basically means without keyboard and monitor). This setup presents us with two challenges if we use a fresh raspbian image for the SD card:

* The Wifi connection is not enabled: The Raspberry Pi don't know how to connect to your WiFi.
* SSH is not enabled: We will use SSH to connect to the Raspberry Pi and continue the setup.

The next steps are based on [vorillaz' blog post](https://dev.to/vorillaz/headless-raspberry-pi-zero-w-setup-3llj) and the [Raspberry Pi installation documentation](https://www.raspberrypi.org/documentation/installation/installing-images/README.md):

* Download the image from the [Raspberry Pi downloads page](https://www.raspberrypi.org/downloads/raspbian/): We will use Raspbian Lite image.
* Writing an image to the SD card: In this example I have used [balenaEtcher](https://www.balena.io/etcher/) for Windows

### Buster Wifi Bug on Raspberry Pi Zero W
Due to [issue 3184](https://github.com/raspberrypi/linux/issues/3184) the wifi configuration doesn't work on the newest release for some configurations. [wpasupplicant needs to be downgraded](https://www.raspberrypi.org/forums/viewtopic.php?f=66&t=244731#p1498661). For the built-in Wifi module a downgrade finally was not required, but adjusting the wpa_supplicant.conf file did the trick. Before the network declaration add the following 3 lines:
```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=PL
```
