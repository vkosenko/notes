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
* fix locale
  * ` sudo locale-gen "en_US.UTF-8" `
  * ` sudo dpkg-reconfigure locales `
* enable ll
  * ` echo "alias ll='ls -lah'" >> ~/.bashrc `
  * ` source ~/.bashrc `
* fix pipe
  * ` sudo vim /etc/default/keyboard `
  * change "gb" to "us" (XKBLAYOUT=”us”)
* install sane
  * check if your device is supported: http://www.sane-project.org/cgi-bin/driver.pl
  * ` sudo apt-get update `
  * ` sudo apt-get install sane-utils ` 
  * check if the device is recognized: ` sudo scanimage -L `
  * download .bin for your scanner: ` wget https://.../snape20.bin ` or get it from the scanner CD
  * create folder to place .bin to: ` sudo mkdir -p /usr/share/sane/snapscan `
  * ` sudo cp ~/snape20.bin /usr/share/sane/snapscan `
  * adjust the firmware in the snapscan config: ` sudo vim /etc/sane.d/snapscan.conf `
    * ` firmware /usr/share/sane/snapscan/snape20.bin ` 
  * set saned to run start automatically:
    * ` sudo vim /etc/default/saned `
    * ` RUN=yes `
    * ` sudo /etc/init.d/saned start `
  * scan image:
    * ` sudo scanimage -d snapscan:libusb:001:004 --format tiff --resolution 150 --mode Gray > test.tiff `
  * add pi user to the scanner group for it to be able to be executed without root
    * ` sudo adduser pi scanner `
  * install ImageMagick to convert from .tiff to .jpeg
    * ` sudo apt-get install imagemagick `
  * convert image
    * ` convert scan.tiff scan.jpg `
  
 