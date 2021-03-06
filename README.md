# Switch DaySkipper
Switch DaySkipper is code based off of bertrandom's snowball thrower, but modified to skip a given amount of days in the switch system to perform glitches across all sorts of games. **Please note that it is currently tuned to the _mm/dd/yy_ format, but I am working on adding the _dd/mm/yy_ format.** The system does not currently work with numbers exceeding 9,223,372,036,854,775,807, but you would die billions of years before it stopped skipping if you set it that high.

### How to use:
#### Setting the # of days to skip
1. Go into the Joystick.c file. 

2. Find the variable at the top that is called "wantDaysSkip" and modify that line to:
long wantDaysSkip = (number of days you want to skip);

3. Save the file.
#### Actually using it
1. Navigate to the switch's Date and Time settings under System Settings>System>Date and Time.

2. Turn off the Synchronize Clock via Internet option in Date and Time.

3. Next, click on the Date and Time option, and ***change the month and day to January 1st***.

4. Finally, navigate to the ok button, and make sure that it is highlighted, plug the controller in (directly to the switch or through the dock) and it should start skipping days.

(the following instructions are from the [project](https://github.com/bertrandom/snowball-thrower) I have forked this from.)
## Wait, what?
On June 20, 2017, Nintendo released System Update v3.0.0 for the Nintendo Switch. Along with a number of additional features that were advertised or noted in the changelog, additional hidden features were added. One of those features allows for the use of compatible USB controllers on the Nintendo Switch, such as the Pokken Tournament Pro Pad.

Unlike the Wii U, which handles these controllers on a 'per-game' basis, the Switch treats the Pokken controller as if it was a Switch Pro Controller. Along with having the icon for the Pro Controller, it functions just like it in terms of using it in other games, apart from the lack of physical controls such as analog sticks, the buttons for the stick clicks, or other system buttons such as Home or Capture.

The original version of the code that this repo is based off of emulated the Pokken Tournament Pro Pad, but changes have been made to support the HORIPAD wired controller for Nintendo Switch instead. In addition, many additional features/improvements have been added.

### Setup
#### Prerequisites
* A LUFA-compatible microcontroller such as the Teensy 2.0++, Arduino UNO R3, or the Arduino Micro
A USB-to-UART adapter.
* In a pinch, an Arduino UNO R3 with the ATMega328p disabled (connect RESET to GND) will work.
* A machine running Linux or MacOS. Currently there are issues running under Windows.
#### Compiling and Flashing onto the Teensy 2.0++
Go to the Teensy website and download/install the Teensy Loader application. For Linux, follow their instructions for installing the GCC Compiler and Tools. For Windows, you will need the latest AVR toolchain from the Atmel site. See this issue and this thread on GBAtemp for more information. (Note for Mac users - the AVR MacPack is now called AVR CrossPack. If that does not work, you can try installing avr-gcc with brew.)

Next, you need to grab the LUFA library. You can download it in a zipped folder at the bottom of this page. Unzip the folder, rename it LUFA, and place it where you like. Then, download or clone the contents of this repository onto your computer. Next, you'll need to make sure the LUFA_PATH inside of the makefile points to the LUFA subdirectory inside your LUFA directory. My Switch-Fightstick directory is in the same directory as my LUFA directory, so I set LUFA_PATH = ../LUFA/LUFA.

Now you should be ready to rock. Open a terminal window in the Switch-Fightstick directory, type make, and hit enter to compile. If all goes well, the printout in the terminal will let you know it finished the build! Follow the directions on flashing Joystick.hex onto your Teensy, which can be found page where you downloaded the Teensy Loader application.

#### Compiling and Flashing onto the Arduino UNO R3
###### You need:
* An arduino UNO R3
* A cable to connect the UNO to the computer and switch
* A jumper wire
#### My experience (windows):

The original instructions weren't very clear, so I figured out a process in windows, and came up with a more in depth set of instructions.

1. Create a folder where you are going to work with this project. 

2. Download the above files and extract them into your premade folder (you may want to create a copy so you don't have to download the files everytime you want to change the days skipped). Refer to [this section](#setting-the--of-days-to-skip) to set the number of days you want to skip.

3. One of the files in the Switch-Dayskipper-Master folder you just extracted is lufa-LUFA-170418.zip, navigate into Switch-DaySkipper-Master and extract lufa-LUFA-170418.zip into the folder you originally created (not the Switch-DaySkipper directory from what you just downloaded). 

4. Now you must download mingw32 from here: http://osdn.net/projects/mingw/downloads/68260/mingw-get-setup.exe/ (it will auto download when you click on the link).

5. Run the file that is downloaded. 

6. Go through the installer until you get to the installation manager.

7. Then click on the box next to mingw32-base-bin and click the "mark for installation" option. 

8. Next go to the installation menu in the top left and click "apply all changes" and then apply. You can now close the dialogue and installation manager. 

9. Next go to https://www.arduino.cc/en/Main/Software, then click on the **Windows Installer** and download arduino (you don't have to donate). 

10. Run the file you've downloaded and go through the installer without changing settings.

11. Using windows explorer, travel to This PC>Local Disk (C:)>Program Files (x86)>Arduino>hardware>tools>avr, **shift right click** on bin, then press "copy as path".

12. After that, press the windows key (opens search bar on left of taskbar) and type "path". 

13. Click on the "edit system environment variables" option, then in the menu it brings up, click on "Environment Variables" button on the bottom right. 

14. Next in the System Variables box click on "Path" and then edit. 

15. After you bring up another menu, click on the "new" button and then ctrl+v (paste) into the text box that is brought up.

16. After that make sure to press ok in all the menus. 

17. Now install Atmel Flip from here: https://www.microchip.com/DevelopmentTools/ProductDetails/PartNO/FLIP. The link will take you to a website that has download options at the bottom, click on the download that says Java Runtime Environment included. 

18. Then run the file that is downloaded and move through the installer without changing anything. 

19. You're almost there! You need to install atmega16u2 drivers here: https://www.driverscape.com/download/atmega16u2 (click on the bottom download, the top one is an ad).

20. Next extract the file (it doesn't matter where).

21. Then plug the arduino in, then briefly connect the two pins closest to the reset button with a jumper cable (you will know when to disconnect when the windows disconected device sound plays).

21. Then go to device manager>other devices and right click on unknown device. 

22. Next click update driver and navigate to the driver you just installed and open it. You can close out device manager.

23. After that, go to This PC>Local Disk (C:)>MinGW>bin and find the mingw32-make.exe file, **shift right click** and click copy as path.

24. Next, go to your folder with the dayskipper files in it, click on the bar with the path and type cmd. 

25. When command prompt opens press ctrl+v (paste) and then press enter.

26. Next, open up flip, and click on the button on the top left (right under the file button) and in the device list find and select the ATmega16U2 option.  

27. Now press ctrl+U then enter, next press ctrl+L and in the window it brings up navigate to the Switch-DaySkipper-Master folder, and double click on the joystick.hex file.

28. Finally press run, and it is ready to go! Just unplug the arduino, close flip and refer to [this section](#actually-using-it)

##### Original instructions:
You will need to set your Arduino in DFU mode, and flash its USB controller. (Note for Mac users - try brew to install the dfu-programmer with brew install dfu-programmer.) Setting an Arduino UNO R3 in DFU mode is quite easy, all you need is a jumper (the boards come with the needed pins in place). Please note that once the board is flashed, you will need to flash it back with the original firmware to make it work again as a standard Arduino. To compile this project you will need the AVR GCC Compiler and Tools. (Again for Mac users - try brew, adding the osx-cross/avr repository, all you need to do is to type brew tap osx-cross/avr and brew install avr-gcc.) Next, you need to grab the LUFA library: download and install it following the steps described for the Teensy 2.0++.

Finally, open a terminal window in the Switch-InputEmulator directory, edit the makefile setting MCU = atmega16u2, and compile by typing make. Follow the DFU mode directions to flash Joystick.hex onto your Arduino UNO R3 and you are done.

#### Compiling and Flashing onto the Arduino Micro
The Arduino Micro is more like the Teensy in that it has a single microcontroller that communicates directly over USB. Most of the steps are the same as those for the Teensy, except do not download Teensy Loader program. You will also need to edit makefile before issuing make. Change MCU = at90usb1286 on line 15 to MCU = atmega32u4.

Once finished building, start up Arduino IDE. Under File -> Preferences, check Show verbose output during: upload and pick OK. With the Arduino plugged in and properly selected under Tools, upload any sketch. Find the line with avrdude and copy the entire avrdude command and all options into a terminal, replacing the .hex file and path to the location of the Joystick.hex created in the previous step. Also make sure the -P/dev/?? port is the same as what Arduino IDE is currently reporting. Now double tap the reset button on the Arduino and quickly press Enter in the terminal. This may take several tries. You may need to press Enter first and then the reset button or try various timings. Eventually, avrdude should report success. Store the avrdude command in a text file or somewhere safe since you will need it every time you want to print a new image.

Sometimes, the Arduino will show up under a different port, so you may need to run Arduino IDE again to see the current port of your Micro.

If you ever need to use your Arduino Micro with Arduino IDE again, the process is somewhat similar. Upload your sketch in the usual way and double tap reset button on the Arduino. It may take several tries and various timings, but should eventually be successful.

The Arduino Leonardo is theoretically compatible, but has not been tested. It also has the ATmega32u4, and is layed out somewhat similar to the Micro.
