# Input Switcher

# 1 - Introduction
The application and scripts provided in this repository let you switch your Logitech keyboard and mouse with one click of a button to another channel. This respository contains scritps for both Windows and Linux.
You can use this repository to create your own specific setup.

# 2 - Windows
The **windows** folder contains the following files:
- switch_to_2.bat
- switch_to_2.vbs
- hidapitester.exe

Create the folling folder **c:\Program Files\InputSwitcher** and copy the 3 files into this folder.
Now use Logitech Options to assign a custom application to the "Menu" key and have it execute the program: C:\Program Files\InputSwitcher\switch_to_2.vbs.

## 2.1 - switch_to_2.bat
This simple batch script switchers the input to channel 2.

# Linux
From the **Linux** folder, copy both files (switch_to_1.sh & hidapitester) to: **\usr\bin**
```
cd linux
sudo cp * \usr\bin
```
Now in your desktop environment of choice, define a custom shortcut. In my case I have used the "Menu" key on my keyboard and assigned it to execute \usr\bin\switch_to_1.sh

hello