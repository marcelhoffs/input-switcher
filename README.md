# Input Switcher

# Introduction
The application and script provided in this repository let you switch your Logitech keyboard and mouse with one click of a button to another channel.

# Windows
The **windows** folder contains the following files:
- switch_to_2.bat (contains the commands to switch keyboard and mouse to input channel)
- switch_to_2.vbs (contains a script to execute the bat file without popping up a command window)
- hidapitester.exe (this is the application that switches the inputs)

Create the folling folder **c:\Program Files\InputSwitcher** and copy the 3 files into this folder.
Now use Logitech Options to assign a custom application to the "Menu" key and have it execute the program: C:\Program Files\InputSwitcher\switch_to_2.vbs.

# Linux
From the **Linux** folder, copy both files (switch_to_1.sh & hidapitester) to: **\usr\bin**
```
cd linux
sudo cp * \usr\bin
```
Now in your desktop environment of choice, define a custom shortcut. In my case I have used the "Menu" key on my keyboard and assigned it to execute \usr\bin\switch_to_1.sh

hello