# Logitech MX - Input Switcher

# 1 - Introduction
The application and scripts provided in this repository let you switch your Logitech keyboard and mouse with one click of a button to another channel. This respository contains scritps for both Windows and Linux. You can use this repository to create your own specific setup.
The repository contains the hidapitester tool for both Windows and Linux.
If you prefer to use the most current version you can download this here: https://github.com/todbot/hidapitester

What you need is 2 Logitech Unifying/Bolt receivers or bluetooth connection. One for your Windows machine and one for your Linux machine. 
Then take one receiver and first connect the keyboard to it and then the mouse. Make sure that both are connected on channel 1.
Take the second receiver and first connect the keyborad to it and then the mouse. Make sure that both are connected on channel 2.
The first receiver connects to the Windows machine, the second to the Linux machine.

So if your keyboard and mouse are on channel 1, they control the Windows machine. If they are on channel 2, they control the Linux machine.

# 2 - Windows
The **windows** folder contains the following files:
- switch_to_2.bat
- switch_to_2.vbs
- hidapitester.exe

Create the following folder **c:\Program Files\InputSwitcher** and copy the 3 files into this folder.
Now use Logitech Options to assign a custom application to the "Menu" key and have it execute the program: **C:\Program Files\InputSwitcher\switch_to_2.vbs**.

## 2.1 - switch_to_2.bat
This simple batch script switches the input to channel 2.

## 2.2 - switch_to_2.vbs
This is a Visual Basic script that is just a wrapper around switch_to_2.bat. If you would execute switch_to_2.bat you would get a command prompt window that pops up every time. The switch_to_2.vbs script prevents this. So if you bind this script to a key on your keyboard you can switch to another channel without windows popping up.

# 3 - Linux
From the **Linux** folder, copy both files (switch_to_1.sh & hidapitester) to: **/usr/bin**
```
cd linux
sudo cp hidapitester /usr/bin
sudo cp switch_to_1.sh /usr/bin
sudo cp 42-logitech-unify.rules /usr/lib/udev/rules.d
chmod +x /usr/bin/hidapitester
chmod +x /usr/bin/switch_to_1.sh
```
If you have Solaar installed copying the 42-logitech-unify.rules file is not needed. If you don't have Solaar installed you will probably notice that hidapitester does not work without root permissions (e.g. via sudo). This is because non-root users do not have raw access to the hid devices by default.
So the 42-logitech-unify.rules file is a udev rule that allows raw access to the Logitech Unify receiver for non-root users. You might have to unplug your receiver and plug it in again.

Now in your desktop environment of choice, define a custom shortcut. In my case I have used the "Menu" key on my keyboard and assigned it to execute **/usr/bin/switch_to_1.sh**.

## 3.1 - switch_to_1.sh
This is a simple shell script for Linux to switch the input to channel 1.

## 3.2 - 42-logitech-unify.rules
As explained earlier, this is a udev rule to allow non-root users raw access to the Unify receiver. As in write commands to it.

# 4 - Mac
To get this working on a Mac refer to [the Mac README](mac/README.md)

# 5 - Bind the scripts to a key
Personally I use this key to bind the scripts to in both Windows and Linux.
![Keyboard](/images/keyboard.png)

## 5.1 - Windows key binding
In Windows you can use Logitech Options to bind the key to the **switch_to_2.vbs** script.

## 5.2 - Linux key binding
In Linux it depends on the desktop environment you use. In Gnome you can do it via: **Settings > Keyboard > View and Customize Shortcuts > Custom Shortcuts**
![Gnome](/images/gnome.png)

### In case the key you want to map is not recognized (GNOME environment)

You can download the awesome [Input Remapper](https://github.com/sezanzeb/input-remapper) tool, which allows you to detect your Logitech devices and more. 
1. Run the tool and click on the device (e.g., Logitech MX Keys) to land in the Presets tab.
2. Create a new Preset, double click it and land into the editor.
3. In the bottom left side of the window, click on the add button below "Input", press "Record" and press the button that you want to remap.
4. In output, you can create a new Macro. Target keybard and press your combination of choice. This combination will be the one that you'll use to trigger the key binding in GNOME. I created something that I will never press: Control_L + Alt_L + Super_L + period
5. Once it has been created, give this preset a name, press the down arrow next to the rename field, and press apply.
6. You now can go in GNOME's custom shortcut editor and specify the script you want to run.
7. Remember to make sure that the script you created is executable and that hidapitester can as root (you have multiple choices, which have a number of security implications -- suid .sh script, sudo nopasswd for hidapitester... make an informed decision)

# 6 - Modify the scripts
Now you know how to set it up, but it probably does not work yet. This is because the delivered script files are geared toward a specific setup.
You will have to figure out what the correct command is that you have to send to your devices for them to switch.

Take the command for Windows for example:  
***.\hidapitester.exe --vidpid 046D:C52B --usage 0x0001 --usagePage 0xFF00 --open --length 7 --send-output 0x10,0x01,0x09,0x1e,0x01,0x00,0x00***

***--vidpid 046D:C52B***  
This is the ID of the Logitech Unifying receiver that is plugged in to the Windows machine. Normally this ID is the same for all receivers. 
In Linux you can easily find this by running the **lsusb** commmand in a terminal.
In Windows you can find the ID via **Devices and Printers**. Find the Logitech Unifying Receiver and check the Hardware ID of the USB Composite Device.
![Devices](/images/find_hardware_id.png)

***--usage 0x0001***  
***--usagePage 0xFF00***  
***--open***  
***--length 7***  
All these options are just defaults, you can ignore those

***--send-output 0x10,0x01,0x09,0x1e,0x01,0x00,0x00***  
This is the important part, because this command tells which device to do what.

Let's take this command: ***0x10,0x01,0x09,0x1e,0x01,0x00,0x00***  
And rewrite it as: ***A,B,C,D,E,F,G***

*A = always 0x10, although Solaar seems to use 0x11.*  
*B = This is the number of the device that is linked to the Unifying receiver: 0x01 for the first device (the keyboard), 0x02 for the second device (the mouse). 0x00 Is supposed to be the Bluetooth device, but I haven't tested that.*  
*C = ?*  
*D = ?*  
*E = This is the channel to switch to: 0x00 for channel 1, 0x01 for channel 2 (and I guess 0x02 for channel 3)*  
*F = always 0x00.*  
*G = always 0x00.*  

So value of C and D are unknown... how to figure that out? Well to do that, we will use the **Solaar** application on Linux.
Install Solaar on Linux and make sure that your keyboard and mouse are connected to channel 2, the Linux machine.
Now open a terminal and execute the following command. This instructs Solaar to switch the device with the name "MX Keys" (the keyboard) to channel 1. So basically you command it to switch the keyboard back to Windows:

*solaar -ddd config "MX Keys" change-host 1*

You should see your keyboard switch to channel 1 and it is connected to Windows again. At the end of the log you will see something like this:

*logitech_receiver.base: (18) <= w[11 01 091E 00000000000000000000000000000000]*

This is the command that was sent, by Solaar, to your keyboard to switch to channel 1.
You can also write this as:

*11 01 09 1E 00 00 00*

or 

*0x11 0x01 0x09 0x1E 0x00 0x00 0x00*

If you repeat this test multiple times you will see that C will never change, it stays 09. Though D will change almost every time. Sometimes it is 1E, sometimes 1B... etc. Just pick one. So finally our set of data, for the keyboard, then is:

*A = 0x10*  
*B = 0x01*  
*C = 0x09*  
*D = 0x1E*  
*E = 0x00 to switch to Windows (channel 1), 0x01 to switch to Linux (channel 2)*  
*F = always 0x00*  
*G = always 0x00*  

Now repeat this for the mouse and you will get this:

*A = 0x10*  
*B = 0x01*  
*C = 0x0A*  
*D = 0x1B*  
*E = 0x00 to switch to Windows (channel 1), 0x01 to switch to Linux (channel 2)*  
*F = always 0x00*  
*G = always 0x00*  

So C is specific to the device. In my case 09 is for the MX Keys keyboard and 0A for the MX Anywhere 3 mouse. This will probably be different in your case.

> ⚠️ If you are having issues getting commands to work on one Windows computer that you extracted from Solaar on another computer, the device number (B) may be different on the different receivers, especially if you have reused a receiver from a different device set. Physically swap the receivers to each computer during testing to verify the numbering.

So in conclusion this is what you have to put in your bat (on Windows) and shell script (on Linux):

**On Windows**  
Keyboard to channel 2 : 0x10,0x01,0x09,0x1e,0x01,0x00,0x00  
Mouse to channel 2    : 0x10,0x02,0x0a,0x1b,0x01,0x00,0x00  

**On Linux**  
Keyboard to channel 1 : 0x10,0x01,0x09,0x1e,0x00,0x00,0x00  
Mouse to channel 1    : 0x10,0x02,0x0a,0x1b,0x00,0x00,0x00  

If you want use bluetooch connection you need to find proper device by using:

***.\hidapitester.exe --list-detail***

then you need to use 11 bytes long message (HID++)

***.\hidapitester.exe --vidpid 046D:B367 --usage 0x0202 --usagePage 0xff43 --open --length 11 --send-output 0x11,0x00,0x09,0x1E,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00***

Keyboard to channel 2: 0x11,0x00,0x09,0x1E,0x01,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00
Mouse (MX Master 3S) to channel 2: 0x11,0x00,0x0A,0x1E,0x01,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00

# 7 Find commands using Wireshark USB capture
It is very easy to capture USB traffic via Wireshark and find commands send to the HID devices. Install [Wireshark](https://www.wireshark.org) including USBPcap and start tracing the USB Hub the dongle is connected. Filter protocol USBHID to find the SET_REPORT request changing the channel or other actions applied to the Logitech device. You can trigger commands using Logitech Options+. The data fragment is excatly the command you need for hidapitester.exe like shown in this example:

**Switch Logitech Craft Keyboard to Channel 3**

*.\hidapitester.exe --vidpid 046D:C52B --usage 0x0001 --usagePage 0xFF00 --open --length 7 --send-output 0x10,0x05,0x08,0x1a,0x02,0x00,0x00*

![Wireshark](/images/wireshark.png)