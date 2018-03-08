##### Prepare the SD Card
* download the image: https://www.raspberrypi.org/downloads/raspbian/
* flash it on the SD card (https://www.raspberrypi.org/documentation/installation/installing-images/mac.md)
  * ` diskutil list `
  * ` diskutil unmountDisk /dev/disk4 `
  * ` sudo dd bs=1m if=2017-11-29-raspbian-stretch-lite.img of=/dev/rdisk4 conv=sync `
* enable SSH
  * ` sudo raspi-config `
  * ` 5 Interfacing options `
  * ` P2 SSH `
  * ` sudo reboot `
 