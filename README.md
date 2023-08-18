# Emulator Detection Bypass steps
Download and setup emulator with any SDK version 12 or below with playstore of x86_64 arch.

# Magisk image flashing[^1]   
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
  
# Setting up frida and other packages in termux[^2]
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
# Frida server installation flow
* Download latest version of frida-server based on device arc type(file name containes server and android) [Link](https://github.com/frida/frida/releases)
* Extract the zip and move the file in you emulator by draging and droping.
* Open root explorer and navigate to root->sdcard->download where you will be able to locate your file.
* Move the file to root->data->local->tmp.
* Rename to file to frida-server
* Long press on the file and select additional options from the top left and select permissions and enable execution rights to all user types.
  <img src="https://github.com/Ms-dev3/EmulatorByPass/assets/111139550/643e5ac9-8fb7-4273-b580-131e19bba2a5" alt="image" width="500" height="550">
* open termux and enter folling commands (When run su command, If App ask for the super permission allow it with press on Grant)
* Goto your app permissions->Additional permmisions->allow Run command in termux terminal(Check below screenshots)
<img src="https://i.imgur.com/OHC7pO5.jpg" alt="Additional permissions" width="230" height="500"> <img src="https://i.imgur.com/J6rcGnQ.jpg" alt="permissions image" width="230" height="500">
* Now to start the server enter following commands.
  ```
  su
  ```
  ```
  cd /data/local/tmp
  ```
  ```
  ls (It will shows you a dir and files of the tmp dir)
  ```
  ```
  ./frida-server -l 127.0.0.1
  ```
  once above command is entered your cursor will move to next line and continue blinking.Leave this session of termux as it is and dont close it.
  To open a new session in termux swipe from the left edge to open a draw and select new session.
* Move emulator bypass js file to root->data->local->tmp
* Now to check if you are able to connect with the server from your new termux session enter below command to list all device process
  ```
  frida-ps -H 127.0.0.1
  ```
  or you can run acutal bypass command as
  ```
  frida -H 127.0.0.1 -f your.packagename -l /data/local/tmp/bypass.js
  ```
  
* If working that our termux setup is complete.
  
# Termux setup to accept external commands.  
* Making termux accept external commands[^3].
  ```
  value="true"; key="allow-external-apps"; file="/data/data/com.termux/files/home/.termux/termux.properties"; mkdir -p "$(dirname "$file")"; chmod 700 "$(dirname "$file")"; if ! grep -E '^'"$key"'=.*' $file &>/dev/null; then [[ -s "$file" && ! -z "$(tail -c 1 "$file")" ]] && newline=$'\n' || newline=""; echo "$newline$key=$value" >> "$file"; else sed -i'' -E 's/^'"$key"'=.*/'"$key=$value"'/' $file; fi
  ```
* Before your app can transmit commands to termux you will have to enable certain permission and make the user grant them.
  ```
  <uses-permission android:name="com.termux.permission.RUN_COMMAND"/>
  ```
  ```
  <queries>
        <package android:name="com.termux" />
        <intent>
            <action android:name="android.intent.action.MAIN" />
        </intent>
  </queries>
  ```
* Sending commands from your app to termux[^4].
  ```
  intent.setClassName("com.termux", "com.termux.app.RunCommandService")
  intent.action = "com.termux.RUN_COMMAND"
  intent.putExtra("com.termux.RUN_COMMAND_PATH", "/data/data/com.termux/files/usr/bin/frida")
  intent.putExtra(
            "com.termux.RUN_COMMAND_ARGUMENTS",
            arrayOf("-H", "127.0.0.1", "-f", "your app package name", "-l", "/data/local/tmp/bypass.js")
  )
  intent.putExtra("com.termux.RUN_COMMAND_BACKGROUND", true)
  intent.putExtra("com.termux.RUN_COMMAND_SESSION_ACTION", "4")
  startService(intent)
  ```
# Additional step
* In case you encounter error while running frida command as below
  ```
  File "/data/data/com.termux/files/usr/lib/python3.11/re/_parser.py", line 455, in _parse_sub itemsappend(_parse(source, state, verbose, nested + 1
  ```
  you can enter following command as mentioned here [Link](https://github.com/frida/frida/issues/2372#issuecomment-1374208979)
  > silverbullet-herr commented Jan 7, 2023
  > 
  > try this:
  > pip uninstall pygments && pip install pygments
  > to install the latest version instead of the required version that's how it worked for me


*References*
[^1]: [Rooting emulator](https://avicoder.me/2021/09/02/Root-AVD-and-install-Magisk/)
[^2]: [Frida setup on termux](https://github.com/frida/frida/discussions/2411)
[^3]: [termux property edit](https://github.com/termux/termux-tasker#allow-external-apps-property-optional)
[^4]: [Frida run commands](https://github.com/termux/termux-app/wiki/RUN_COMMAND-Intent)


