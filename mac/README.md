# Logitech MX - Input Switcher instructions for Mac

## Summary
There is one script provided, `switch.sh`. This same script needs to be deployed across as many Mac computers as you are controlling via MX Mouse and Keys. You only need to make changes to `KYB_CH`, `KYB_ID`, `MSE_CH` and `MSE_ID` depending on your configuration. Please read the comments. You should not have to change the `RCVR_PID` and `RCVR_VID` variables but always good to check as described in the comments.

## How to install 
- From the **osx** folder, copy file `switch.sh`  and `hidapitester` to `/usr/local/bin` (make sure `/usr/local/bin` is in your PATH)
- Open up Finder, navigate to `/usr/local/bin`, right click on `switch.sh` and select 'Get Info'. In the 'Open with' row, make sure you select your terminal app. Note that the default OSX terminal App (`Terminal.app`) is sitting inside `/Applications/Utilities`. You'll have to select Other->Enable All Applications, go inside the utilities folder and select `Terminal.app`. I like to use this terminal, and in the terminal app preferences (Terminal->Preferences->Shell) select 'Close the window' inside the 'Shell' tab. That way, when the script is launched, the shell window closes. 

What you have basically done above is to make sure if the file is 'opened' it will be executed in the terminal. This is needed to link it to the logitech app. There are other ways like converting the script to an 'app' or using automator. I found this to be the simplest.

**Note:** If you are not able to run the bundled hidapitester executable (security permissions), you can either go to your security settings (System Preferences->Security & Privacy) and allow the application to be run, or,  follow instructions [here](https://github.com/todbot/hidapitester) to compile your own version.

## Modify the script

You'll need to modify the script to point to the right channels and device IDs. Please read the comments inside the script as well as [the main README section](https://github.com/marcelhoffs/input-switcher#5---modify-the-scripts) on values to use
## Test it
Before you do any keyboard automation, try running `switch.sh` from your command line. If your keyboard and mouse don't transfer over, you need to change 
the variables. When you are sure the script works, move to the next step.

## Bind to keyboard and/or mouse
I like to use my central mouse button to switch as well as my calculator key on the keyboard. You can select other buttons

### Bind to MX Keys
Go to your 'Logi Options+ app', click on your keyboard, select the key you want to override, in actions, select 'Open an application' and put in `/usr/local/bin/switch.sh`. Because you associated this script to your terminal app, it will be executed when you press the key.

### Bind to MX Mouse
Go to your 'Logi Options+ app', click on your mouse, select the mouse button you want to override, in actions, select 'Open an application' and put in `/usr/local/bin/switch.sh`. Because you associated this script to your terminal app, it will be executed when you press the key. Note that I've found mouse integration iffy. Depending on which window you are focussed on, and what mouseevents it grabs, this may not always reliably work. Keyboard integration works all the time.

