# Emulator Detection Bypass steps
Download and setup emulator with any SDK version 12 or below with playstore of x86_64 arch.

# Get magisk image flashing repo 
* Download and extract rootAVD repo from this [Link](https://github.com/newbit1/rootAVD)
* Open terminal on your pc and navigate to above extracted dir.
* trigger command as
  ```
  ./rootAVD.sh
  ```
* This will list you commands that you need to trigger.
* Trigger command
  ```
  ./rootAVD.sh ListAllAVDs
  ```
  and select the image matching your emulators matching arch type.
* Once flashing is done it should reboot your emulator.
* Trigger command
  ```
  ./rootAVD.sh InstallApps
  ```
* Once done your emulator will have magisk installed in it,start the application it will ask permission which will then reboot your device.
* Once device has rebooted go to magisk settings and enable zygisk setting and reboot your device from magisk options.
* You are now done flashing/rooting your deivce.
# Setting up termux on device.
* Download latest apk from termux repo release section based on your emulator arch type [Link](https://github.com/termux/termux-app/releases)
* Open the app and enter command
  ```
  pkg update
  ```
* Once above is done enter command
  ```
  pkg upgrade
  ```
* Enter command
  ```
  termux-setup-storage
  ```
  and grant storage permission.
* Your termux is not ready to use.
  
# Additional Apps/tools that are needed
* Download and install root explorer apk.
  
# Setting up frida and other packages in termux
* Enter command
  ```
  pkg install build-essential python python-pip git wget binutils openssl
  ```
*  Download Frida Core DevKit according to device architecture from [Link](https://github.com/frida/frida/releases)
*  Extract the zip and move the fils in your emulator (there will be 4 files)
*  Open root explorer and navigate to root->sdcard->downloads you will be able to locate your files that you had recently copied to this device.
*  Move these files to root->sdcard->devkit(make a new dir).
*  Open termux and enter command
  ```
export FRIDA_CORE_DEVKIT=/sdcard/devkit/
```
   if you extracted it on some other location, use that path.make sure you run above command without root/su.
* Install frida and its commandline tools from pip
  ```
  pip install frida frida-tools
  ```
  ![image](https://user-images.githubusercontent.com/27184655/218310575-89d7d2c0-028d-4942-a5ea-edc96461d55f.jpg)
  Now Frida is available to use from commandline.you can check version by typeing ``` frida-ps --version ```
* Optional steps if with above frida is giving error.
  ```
  pkg install root-repo
  ```
  ```
  pkg install frida-python
  ```
# [Frida server installation flow](https://github.com/frida/frida/discussions/2411)
* Download latest version of frida-server based on device arc type [Link](https://github.com/frida/frida/releases)
* Extract the zip and move the file in you emulator by draging and droping.
* Open root explorer and navigate to root->sdcard->download where you will be able to locate your file.
* Move the file to root->data->local->tmp.
* Rename to file to frida-server
* Long press on the file and select additional options from the top left and select permissions and enable execution rights to all user types. ![image](https://github.com/Ms-dev3/EmulatorByPass/assets/111139550/643e5ac9-8fb7-4273-b580-131e19bba2a5)
* open termux and enter folling commands
  ```
  su
  ```
  ```
  cd /data/local/tmp
  ```
  ```
  ./frida-server -l 127.0.0.1
  ```
  once above command is entered your cursor will move to next line and continue blinking.Leave this session of termux as it is and dont close it.
  To open a new session in termux swipe from the left edge to open a draw and select new session.
* Now to check if you are able to connect with the server from in your new termux session enter below command to list all device process
  ```
  frida-ps -H 127.0.0.1
  ```
* If working that our termux setup is complete.
  
# Termux setup to accept external commands.  


