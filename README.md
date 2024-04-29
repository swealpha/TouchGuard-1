# TouchGuard

Disables Mac touchpad for a user-specified amount of time each time a key is pressed on the keyboard. This prevents accidental touchpad input (e.g. palm of hand moving over the edge of the touchpad) from being detected as a tap and causing the cursor to jump to a different line while the user is typing.

**Download latest release from [here](https://github.com/thesyntaxinator/TouchGuard/releases)**

*NOTE: Must be run with administrative privileges.*

----------------
## Usage (non-tech savvy)
- Open Terminal, type "chmod +x ", drag the drop the downloaded file into the Terminal window, and press enter (this only needs to be done once after downloading the file).
- Then type "sudo", drag and drop the downloaded file into the Terminal window, type " -time 0.2" and press enter. You may be prompted for your password; if so, type it and presss enter. Note that you will not see the cursor move while typing your password -- this is normal and done for security reasons.
- Keep the terminal window open. If you close the window, the program will exit. You can hide the window by typing "command-h".
- You will need to manually relaunch the app each time you restart your computer using the above sequence of steps. To auto-start after you restart your computer, see an unofficial extension of the project at <a href="https://github.com/amanagr/TouchGuard" target="_blank">amanagr/TouchGuard</a>.

------------------
## Sample command line usage (for the more tech-savvy)
```
# make the downloaded release file executable
chmod +x TouchGuard
# run it
sudo ./TouchGuard -time 0.2
```

The above launches TouchGuard with a time interval of 200 ms (disables the touchpad for 200 ms each time a key is pressed on the keyboard). I have found this to be effective for me -- if you are still having issues (e.g. you can't use the trackpad immediately after typing, or your cursor still jumps), you can adjust the time interval up or down as needed.

*Note: You will need to manually relaunch the app each time you restart your computer. A future goal is to create an installer with an option to automatically run the program (with elevated privileges) every time the computer starts. If you would like to work on this, feel free to fork the project and let me know if you get it working (see contact info under "Support" below).*

----------------
## Support
Questions? Comments? Feedback? Issues? Open a new issue [here](https://github.com/thesyntaxinator/TouchGuard/issues) or email syntaxsoftsupport@icloud.com.




________________________________________________
Here is a guide on how to autostart touchguard.

Guide on how we got it up and running on Mac M3 Sonoma 14.4.1

________________________________________________
1.
Put both files “runtouchguard” and “touchguard” in the “Users/admin/” folder.
(NOTE! Admin is my username on the macOS account)
________________________________________________

(NOTE! ""runtouchguard" should contain this below and have no extension.)

#!/bin/sh

PATH_TO_THIS_DIR="$(dirname $(realpath $0))"

sudo "$PATH_TO_THIS_DIR/touchguard" -time 0.5

________________________________________________
2.
Open terminal when you are in the same folder as both files.
i.e. "User/admin/"

Make both files executable by typing this in the terminal separately.
The icons of the files in the folder change to Unix executables.

chmod +x runtouchguard

chmod +x touchguard

________________________________________________

Open terminal and run “sudo visudo”
Navigate down with the arrow keys until you find these 3 lines:

#root and users in group wheel can run anything on any machine as any user

root   ALL = (ALL) ALL

%admin ALL = (ALL) ALL

stand on the empty line below the line starting with '%admin' and
press the letter "i" (which is an insert function in terminal).
Then add this line:

admin ALL = NOPASSWD: /Users/admin/touchguard


Should look like this:

#root and users in group wheel can run anything on any machine as any user

root   ALL = (ALL) ALL

%admin ALL = (ALL) ALL

admin  ALL = NOPASSWD: /Users/admin/touchguard


Then save by pressing ESC,W,ESC,Q. Get it confirmed with "written".
________________________________________________

4.
Now go to the folder "Users/admin/" and run the file runtouchguard with You will probably have to allow to bypass the script with the MacOS system settings "privacy and security". Now it should work!

________________________________________________

5.
To add "runtouchguard" to start automatically with macOS:

Open System Preferences -> General -> Startup Items.

Press the plus sign "+" and select the file "runtouchguard".

Restart and test that everything works with autostart and touchguard!

________________________________________________

Extra:
You can experiment with how many milliseconds the touch should be off after pressing the keyboard.

For that, change "-time 0.5" to e.g. "-time 0.3" in the file "runtouchguard".

#!/bin/sh

PATH_TO_THIS_DIR="$(dirname $(realpath $0))"

sudo "$PATH_TO_THIS_DIR/touchguard" -time 0.5
