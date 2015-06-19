## Install openocd
* Install libftdi
`sudo apt-get install libftdi-dev`
* Download the source package [openocd](http://sourceforge.net/projects/openocd/files/openocd/0.7.0/openocd-0.7.0.tar.gz/download)
* Install it
  * `./configure --enable-ft2232_libftdi`
  * `make`
  * `sudo make install`
* Add new file 99-ti-launchpad.rules in /etc/udev/rules.d/
  
   `# CC3200 LaunchPad
      SUBSYSTEM=="usb", ATTRS{idVendor}=="0451", ATTRS{idProduct}=="c32a", MODE="0660", GROUP="dialout",
      RUN+="/sbin/modprobe ftdi-sio" RUN+="/bin/sh -c '/bin/echo 0451 c32a > /sys/bus/usb-serial/drivers/ftdi_sio/new_id'"`
* Restart udev
   * `sudo service udev restart`
    
## Download and install gcc-arm-embedded following [gcc arm](https://launchpad.net/gcc-arm-embedded)
    
## Download and install using wine CC3200 SDK

## Load an example program
* `cd ~/.wine/drive_c/TI/CC3200SDK_1.1.0/cc3200-sdk/example/getting_started_with_wlan_station/gcc/`
* `make`
* `cd ../../../tools/gcc_scripts/`
* `sudo openocd -f cc3200.cfg`
* exit using ctrl + c
* `cp ~/drive_c/TI/CC3200SDK_1.1.0/cc3200-sdk/example/getting_started_with_wlan_station/gcc/exe/wlan_station.axf .`
* Start serial terminal: `sudo minicom -D /dev/ttyUSB1`
* Start the application: `arm-none-eabi-gdb -x gdbinit wlan_station.axf`
