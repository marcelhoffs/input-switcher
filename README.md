# Input Switcher

# 1 - Introduction
The application and scripts provided in this repository let you switch your Logitech keyboard and mouse with one click of a button to another channel. This respository contains scritps for both Windows and Linux. You can use this repository to create your own specific setup.
The repository contains the hidapitester tool for both Windows and Linux.
If you prefer to use the most current version you can download this here: https://github.com/todbot/hidapitester

# 2 - Windows
The **windows** folder contains the following files:
- switch_to_2.bat
- switch_to_2.vbs
- hidapitester.exe

Create the folling folder **c:\Program Files\InputSwitcher** and copy the 3 files into this folder.
Now use Logitech Options to assign a custom application to the "Menu" key and have it execute the program: C:\Program Files\InputSwitcher\switch_to_2.vbs.

## 2.1 - switch_to_2.bat
This simple batch script switchers the input to channel 2.

## 2.2 - switch_to_2.vbs
This is a Visual Basic script that is just a wrapper around switch_to_2.bat. If you would execute switch_to_2.bat you would get a command prompt window that pops up every time. The switch_to_2.vbs script prevents this. So if you bind this script to a key on your keyboard you can switch to another channel without windows popping up.

# 3 - Linux
From the **Linux** folder, copy both files (switch_to_1.sh & hidapitester) to: **\usr\bin**
```
cd linux
sudo cp * \usr\bin
```
Now in your desktop environment of choice, define a custom shortcut. In my case I have used the "Menu" key on my keyboard and assigned it to execute \usr\bin\switch_to_1.sh

## 3.1 - switch_to_1.sh
This is a simple shell script for Linux to switch the input to channel 1.

# 4 - Bind the scripts to a key
Personally I use this key to bind the scripts to in both Windows and Linux.
![Keyboard](/images/keyboard.png)

## 4.1 - Windows key binding
In Windows you can use Logitech Options to bind the key to the **switch_to_2.vbs** script.

## 4.2 - Linux key binding
In Linux it depends on the desktop environment you use. In Gnome you can do it via: **Settings > Keyboard > View and Customize Shortcuts > Custom Shortcuts**
![Gnome](/images/gnome.png)

# 5 - Detailed setup
Now you know how to set it up, but it probably does not work yet. This is because the delivered script files are geared toward a specific setup.
You will have to figure out what the correct command is that you have to send to your devices for them to switch.

Take the command for Windows for example:
*.\hidapitester.exe --vidpid 046D:C52B --usage 0x0001 --usagePage 0xFF00 --open --length 7 --send-output 0x10,0x01,0x09,0x1e,0x01,0x00,0x00*

*--vidpid 046D:C52B  *
This is the ID of the Logitech Unifying receiver that is plugged in to the Windows machine. Normally this ID is the same for all receivers. 
In Linux you can easily find this by running the **lsusb** commmand in a terminal.
In Windows you can find the ID via **Devices and Printers**. Find the Logitech Unifying Receiver and check the Hardware ID of the USB Composite Device.
![Devices](/images/find_hardware_id.png)

*--usage 0x0001  
--usagePage 0xFF00  
--open  
--length 7  *
All thes options are just defaults, you can ignore those

*--send-output 0x10,0x01,0x09,0x1e,0x01,0x00,0x00*
This is the important part, because this command tells which device to do what.

