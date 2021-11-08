# Input Switcher

# Introduction


# Windows
Fro the Windows, copy all files (switch_to_2.bat, switch_to_2.vbs & hidapitester.exe) to c:\Program Files\InputSwitcher.
Now use Logitech Options to assign a custom application to the "Menu" key and have it execute the program: C:\Program Files\InputSwitcher\switch_to_2.vbs.

# Step 3: Install Desktop Environment
From the Linux folder, copy both files (switch_to_1.sh & hidapitester) to: \usr\bin
```
cd linux
sudo cp * \usr\bin
```
Now in your desktop environment of choice, define a custom shortcut. In my case I have used the "Menu" key on my keyboard and assigned it to execute \usr\bin\switch_to_1.sh