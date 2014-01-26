This is a fork of Universal GcodeSender for TinyG. 

There have been some basic modifications made to support the JSON format that TinyG uses as
well as the unique model that TinyG uses for sending back responses when a command has been
processed. Typically CNC controllers accept one Gcode command and when you get a newline
response from the controller the command has been accepted. Instead on TinyG you can
send in multiple commands for the planner to do its work, but then mapping the responses back
from TinyG to the front-end UI is a bit more work. This fork solves that.

There are items that don't work that haven't been wired up yet, like showing you the current
XYZ position of TinyG. You have to instead just send the "pos" command to TinyG from the
TinyG tab. I created some buttons to send those commands easily. You can also send direct 
JSON commands from the command tab of UGS. For example, just type "?" in the command window
and you'll get position info back from TinyG. If you type in Gcode, I also wrap it in JSON
for TinyG when you do so. 

Also, as I have found on my Shapeoko, I need to turn the motors on before a job starts so 
that I don't lose position while milling. I then turn off the motors by turning Power Mgmt
back on when the job is finished. Don't forget to send some movement commands to your motors
after you turn power mgmt back on or the TinyG won't put the motors into sleep mode.

TinyG tab inside UGS
![Command table tab during a file send](https://github.com/johnlauer/Universal-G-Code-Sender/raw/master/pictures/tinygtab.png "Tab inside UGS for TinyG commands.")

To run this code I simply open it inside Netbeans and hit Run from Netbeans. I do not run it from 
the compiled version as I found that it's easier to do it inside Netbeans. Also, if you want to 
tweak any commands it's easier to do by modifying the source and re-running.

-John

Here's the original readme content for UGS below...

Universal GcodeSender is a Java based GRBL compatibl cross platform G-Code sender. 
Use this program to run a GRBL controlled CNC machine.

To run simply unzip the .zip file and double click the .jar file.
On some platforms you will need to run an included start script.

Note for MAC users:
You may need to create a "/var/lock" directory on OSX to fix a bug in the serial
library. To do this open the Terminal application and run the following two
commands:
<br />
   sudo mkdir /var/lock
<br />
   sudo chmod 777 /var/lock
<br />

Downloads
---------
[1.0.6](http://bit.ly/16q7obd)
<br />
[1.0.5 32-bit](http://bit.ly/Xz4U1R)
<br />
[1.0.5 64-bit](http://bit.ly/SGKfMN)
<br />
[Older releases can be found on the downloads page](https://github.com/winder/builds/tree/master/UniversalGCodeSender)
<br />

![Command table tab during a file send](https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/1.0.6_command_table.png "Command table tab during a file send.")
![3D Visualizer Window](https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/1.0.6_visualizer.png "Visualizer window during a file send.")
![Finished sending a file](https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/1.0.6_job_finished.png "Popup after finishing a file send.")
![Finished sending a file](https://github.com/winder/Universal-G-Code-Sender/raw/master/pictures/1.0.6_advanced_machine_control.png "Advanced GRBL control buttons.")

Technical details:
* RXTX for serial communication.
* JogAmp for OpenGL.
* Utilizes One-Jar to bundle all dependencies into a single runnable .jar file.
* Developed with NetBeans 7.2.1 or later.
* For development you will need to install RXTX.
* To build a release open the 'Files' pane and right click build.xml, then 
  select 'Run Target' > 'onejar-build-release'. A new directory named 'release'
  will contain the .zip file.

Changelog
---------
1.0.5 -> 1.0.6
* 3D gcode visualizer!
* - color coded line segments
* - real time tool position
* - real time gcode buffer position
* Due to popular demand, RaspberryPi support.
* Complete all-in-one release, 32 and 64 bit linux/windows/mac + RaspberryPi
* Settings saved between runs (thanks lazyzero)
* Major backend refactoring to make code more stable and testable.
* Unit tests added, over 1300 lines of unit test code.
* Tinyg support now included. Thank you John Lauer.

1.0.4 -> 1.0.5
* Job duration estimate now displayed when running a file.
* Real-time machine position display for GRBL v8.0c.
* Display for most recent GcodeComment.
* Bug fixes - no more dropped commands!
* Overhauled the GUI to display more information.

1.0.3 -> 1.0.4
* The step size spinner now goes to less than 1.
* New buttons on the manual control page for common functions.
* Manual X/Y coordinates can now be modified with arrow keys.
* New start scripts added to release zip files.
* Changed speed override to a percentage rather than absolute.
* Bug fixes.

1.0.2 -> 1.0.3
* Manual jogging mode, control machine with buttons in the UI.
* Automatically skip blank lines and comments when sending a file.
* Bug fixes.

1.0.1 -> 1.0.2
* Grbl version checking.
* Real-time pause/resume commands used for Grbl v0.8.
* Comment filtering - parses out comments before sending commands.
* Bug fixes.

1.0 -> 1.0.1
* New distribution jar - Application no longer requires RXTX to be installed!
* Added table view for file streaming.
* Added Pause/Resume button.
* Usability improvements.
* Many bug fixes.
* Renamed package to com.willwinder.universalgcodesender.
