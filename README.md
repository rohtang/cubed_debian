The Cube i9 is a decent portable computing device that recently came out of Shenzen, China. It comes bundled with Windows 10, but installing debian is thankfully straight forward.
Stick your favourite flavour of debian on an USB thumb drive, plug it in along with a keyboard, and boot off the USB. I've installed stretch on mine. Wheezy does not play ball as the kernel locks early in the boot process.

Most things are working straight away, including the cover keyboard and touchpad. Additionally, the touchscreen, sound, and all physical buttons are working out of the box with the stock kernel. 

Some things, however, are not working:
- WLAN
- Bluetooth
- Auto rotation

Additionally, the battery drain will be slightly higher compared to W10 - this however, is no fault of the cube itself, but rather flaky power management support in the kernel for the skylake family:
[https://mjg59.dreamwidth.org/41713.html](https://mjg59.dreamwidth.org/41713.html)

Getting WLAN to work:

Obtain an internet connection somehow (I tethered my android phone via USB)

run
```
# apt-get install build-essential linux-headers
clone in to the rtl8723bu repo:
$ git clone https://github.com/lwfinger/rtl8723bu.git
$ cd rtl8723bu
$ make
# make install
# modprobe 8723bu
```
... and there you have it.

Getting bluetooth to work:

all that's missing is the FW for the chipset.
You'll need to enable the non-free repos, and just run
```
# apt-get install firmware-realtek
```

reboot or re-insert the module, and BT will work.

Auto rotation and automatically changing display orientation:

Working on it.
