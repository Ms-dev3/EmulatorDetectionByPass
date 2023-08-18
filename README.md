# EmulatorByPass
Download and setup emulator with any SDK version 12 or below with playstore of x86_64 arch.
# Get magisk image flashing repo 
* Download and extract rootAVD repo from this [Link](https://github.com/newbit1/rootAVD)
* Open terminal on your pc and navigate to above extracted dir.
* trigger command as ```./rootAVD.sh```
* This will list you commands that you need to trigger.
* Trigger command ```./rootAVD.sh ListAllAVDs``` and select the image matching your emulators matching arch type.
* Once flashing is done it should reboot your emulator.
* Trigger command ```./rootAVD.sh InstallApps```.
* Once done your emulator will have magisk installed in it,start the application it will ask permission which will then reboot your device.
* Once device has rebooted go to magisk settings and enable zygisk setting and reboot your device from magisk options.
* You are now done flashing/rooting your deivce.
# Setting up termux on device.
* Download latest apk from termux repo release section based on your emulator arch type [Link](https://github.com/termux/termux-app/releases)
* Open the app and enter command ```pkg update```
* Once above is done enter command ```pkg upgrade```
* Enter command ```termux-setup-storage``` and grant storage permission.
* Your termux is not ready to use.
# Additional Apps/tools that are needed
* Download and install root explorer apk.
# Setting up frida and other packages in termux
* enter command ``` pkg install build-essential python python-pip git wget binutils openssl ```
*  Download Frida Core DevKit according to device architecture from [Link](https://github.com/frida/frida/releases)
*  Extract the zip and move the fils in your emulator (there will be 4 files)
*  Open root explorer and navigate to root->sdcard->downloads you will be able to locate your files that you had recently copied to this device.
*  Move these files to root->sdcard->devkit(make a new dir).
*  open termux and enter command ```export FRIDA_CORE_DEVKIT=/sdcard/devkit/```


