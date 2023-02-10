# APSKY3D-SV05-2.1.2
Marlin 2.1.2 with input shaping enabled for the Sovol SV05

This version incorporates the configuration changes originally made by RoryGame in version 2.1.x
The list of feature enabled is below, as per Rory's original documentation.
Some features in this version do not work (notably cancel object), hopefully someone will help and double check.

Rory Game original Readme file

BE AWARE THERE ARE EXPERIMENTAL FEATURES IN USE

USE AT OWN RISK

BL Touch TURBO Mode!

This means the probe needle will NOT retract when in use! Be sure
that there are NO obstructions on the bed or the printer WILL be
damaged!

You have been warned, use at your own risk, I accept no
responsibility or liability for any damage caused by using this
firmware.

Pre compiled Marlin 2.1.x firmware for use on a completely
stock Sovol SV05

When you come to use the firmware for the first time cover
the power switch in case you need to turn the printer off
quickly.

Add the “firmware.bin" file directly to your printer's SD card root
directory. Do not change the extension! Don’t put it in a folder & be
sure to remove from the .zip folder it came in! With the printer off
insert the card & power on, the screen will be blank for 10-20
seconds then your new system will boot.


!!!VITALLY IMPORTANT!!!

MPC Hotend temperature control

You MUST tune the MPC system BEFORE you use the hotend
heater or it will cause an error & halt the printer.
To do this go to:

Configuration Menu / Advanced Settings / Temperature / MPC
Autotune


This will make the printer do some weird stuff, but it’s ok as it’s just
the printer learning.

It’ll home the printer, then jump low to the bed, start the fan & cool
until minimum temperature is reached, then it’ll start heating. Once
done it’ll heat a little higher & test thermal losses & start the fan
again.

Leave this Process to finish. It will end when the nozzle raises back
off the bed.


You MUST then go to:
Configuration Menu / Store Settings

Then go back to:
Configuration Menu / Advanced Settings / Temperature / Bed PID
Autotune 60

select your normal printing temp for the BED & click the screen
button.

The printer will look like it didn’t work, but the bed heater will come
on & get to temp then heat 5 times. Let this complete & store
settings as per above.


Bed Tramming
You must then set the bed tramming with either the Tramming
Wizard or the Bed Tramming options in the Motion menu.
The Tramming Wizard is very good, its best if the bed is heated to
your preferred temperature, then select point 1, this is your
reference point, all other points are to this point. You have to click
measure & then it will read 0.00. Now click done & move to your
next point, click measure & adjust the bed wheel a little & measure
again until it also reads 0.00 or close to it. Then move to the next
point, be aware each corner you move effects the opposite corner
so it can be good to go round 2 or 3 times to get the best result.


Z Probe Offset

This is vital to a good print, first you must heat the printer to your
full normal printing temperature for both the bed & the nozzle, then
navigate to Configuration Menu / Advanced Settings / Probe
Offsets / Z Probe Wizard.

Click the wizard & it will start, if you haven’t heated the printer it will
do it cold & this is incorrect, be sure its heated up.
Now grab a single unfolded piece of copy paper & place it under
the nozzle & carefully lower the nozzle down to pinch the paper.

BE CAREFUL here as you can crash the nozzle into the bed!!!
Use the large increments down to a height of 4mm then change to
the smallest increment for the last 4mm.
You want the nozzle to drag on the paper enough so it can be
pulled towards you but only just pushed away from you without
stopping & folding up in front of the nozzle.

Once you have this click DONE, the printer will set & save
your new Z offset. If you like you can manually Store Settings
to be sure.


UBL Mesh Building

To build a suitable UBL mesh you go to the Motion menu & click
Unified Bed Levelling & then on to UBL Wizard, set your preferred
bed temperature, don’t worry about the nozzle temp. Choose slot 0
& start the Wizard.

The printer will now probe your bed, it won’t get all the points so
don’t worry about that, its due to firmware safety margins &
mechanical limits of your printer.

Once completed go into the UBL menu & select Step by Step UBL,
now click option 2, Smart Fill-in. The printer won’t do anything
other than make a funny noise at you, but is working. Click it 2 or 3
times. What this is doing automatically filling in all the gaps of the
mesh, the ones the printer couldn’t reach. It does this by using the
data points next to & around the missing points.
Now, go back to the Configuration Menu & Store Settings, if you
forget to do this your hard work here will be lost!!
Then you must add these three lines into your Start G code
in your slicer for it to all work:

These MUST go in after your G28 commands & after your bed has
warmed up, but before you print any purge lines.

G29 A ; Unified bed-level (BL-Touch)

G29 L0 ; Load Mesh Slot 0

G29 J3 ; Probe 9 points to check mesh

This will make the UBL system work for each print.

Also add this line into your Slicer's filament G code section:

M900 K(x.xx)

Replace "(x.xx)" without the brackets with your tuned K value for
Linear Advance for that filament So for example M900 K0.10 To
tune your Linear Advance go here to setup your print calibration
file... https://marlinfw.org/tools/lin_advance/k-factor.html There are
many new features enabled in this firmware. Also linear advance
info page https://marlinfw.org/docs/features/lin_advance.html


Be sure to calculate your E Steps.

Slow double click encoder wheel for Z Move shortcut when not
printing. Slow double click encoder wheel for Babysteps Z with
displayed total while printing. Assisted Tramming Wizard. Linear
Advance. Mesh Wizard. Offset Wizard. Park on Pause!! Save
Position & Resume. Plus many more, including 3 hidden games.
These files are provided as is, use at your own risk.
Manual & pinout info here. https://github.com/bigtreetech/
BIGTREETECH-SKR-mini-E3/tree/master/hardware/
BTT%20SKR%20MINI%20E3%20V3.0/Hardware
Helpful video here. https://m.youtube.com/watch?
v=VxCBDyvFSgA


Marlin Cancel Object

This is a new feature in these builds.
To use with Cura it should be simple as it “should’ have everything
ready to go.

For use with PrusaSlicer you need to do a few things…
First you need to download this https://github.com/paukstelis/
PrusaSlicer-M486 & place it in your chosen folder on your
computer.
Then in PrusaSlicer you must go to the “Print Settings” tab, enable
expert mode & check the box for “Label Objects” in the “Output
File” section.
After that you must enter the file path to the Python program you
just downloaded from the link above in the “Post-processing
scripts” box at the bottom.
*Example* /users/me/documents/prusaslicer/m486.py;
Then you have to save the print setting config in the slicer.
Next, if you’re using a Mac you will have to install Command Line
tools. To do that go up to the “Go” menu bar item & select
“Utilities”, then once there double click the “Terminal” app, The
black TV screen looking one.
Then paste in this: xcode-select --install
Press return to execute.
You may need to do it a couple of times, until it asks you if you
want to download it.
Once that’s done restart the Mac.
Lastly (Phew!) go here…
https://www.python.org/downloads/macos/
& install the latest Python3 & after the install be sure to double click
these files to update your machine:
Install Certificates.command
Update Shell Profile.command
Now you should be able to see individual objects in the new printer
menu item & cancel them directly on the printer which was not
possible before.

