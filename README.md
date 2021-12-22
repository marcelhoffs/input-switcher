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

4 - Bind the scripts to a key
Personally I use this key to bind the scripts to in both Windows and Linux.
![Keyboard](/images/keyboard.png)