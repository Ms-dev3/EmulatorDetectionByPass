# EmulatorByPass
Download and setup emulator with any SDK version 12 or below with playstore of x86_64 arch.
# Get magisk image flashing repo 
* Download and extract rootAVD repo from this [Link](https://github.com/newbit1/rootAVD)
* Open terminal on your pc and navigate to above extracted dir.
* trigger command as ```./rootAVD.sh```
* This will list you commands that you need to trigger.
* Trigger command ```./rootAVD.sh ListAllAVDs ``` and select the image matching your emulators matching arch type.
* Once flashing is done it should reboot your emulator.
* Trigger command ```./rootAVD.sh InstallApps ```.
* Once done your emulator will have magisk installed in it,start the application it will ask permission which will then reboot your device.
* Once device has rebooted go to magisk settings and enable zygisk setting and reboot your device from magisk options.
* You are now done flashing/rooting your deivce.
