# Self-Driving-Donkey-RC-Car-Project
My goal for this project: Utilize, learn, and expand on the real-life application of machine learning/AI. 

This isn't fully deisgned by me; I researched and utilized multiple codes, instructions, and APIs from online. 

However, I don't plan to stop my machine learning interest here. For my next project, I look forward to explore deep into
neutral networks and create a program that can take limitless senory input functions (ultra-sonic, color, or even vision) and create
output layers beyond moving (e.g. lifting arm).

Next project: Build a Sumo bot with a artificial brain



----->








**Starting from below is my Journal :)**

# 3/21/20 - Gathering data, Training, and autopilot

*   Useful commands:
    *   `nano ~/mycar/myconfig.py `- Access to the speculation (steering & throttle, etc) file for calibration
    *   `donkey calibrate --channel &lt;your_steering_channel> --bus=1 `- Throttle calibration measurement testing
    *   `donkey calibrate --channel &lt;your_throttle_channel> --bus=1 - `Steering calibration measurement testing
    *   `cd ~/mycar`
    *   `python manage.py drive`
    *   `&lt;your car's hostname.local>:8887`
    *   `Scp `command
*   Notes (Steps):
    *   Created a track using multiple thin line of papers
    *   After starting my car with `python manage.py drive`command and going on at the URL  `&lt;your car's hostname.local>:8887`to control, start recording and drive around 10 laps.
    *   To transfer data from raspberry pi to my windows computer, use  “scp” command instead “rsync” command for windows PC
    *   Command (for Linux): `rsync -rv --show-progress --partial pi@&lt;your_pi_ip_address>:~/mycar/data/  ~/mycar/data/`
    *   Command(for windows): `scp pi@&lt;your_pi_ip_address>:~/mycar/data/  \mycar\data\`
    *   Using your host PC (windows PC for my case), train a model using the data with the command
    *   Command (for linux): `python ~/mycar/manage.py train --tub &lt;tub folder names comma separated> --model ./models/mypilot.h5`
    *   Command (for windows): `python \mycar\manage.py train --tub &lt;tub folder names comma separated> --model .\models\mypilot.h5`
    *   After completing the training process, copy the model back to the raspberry pi(car)
    *   Command (for linux): `rsync -rv --show-progress --partial ~/mycar/models/ pi@&lt;your_ip_address>:~/mycar/models/`
    *   Command (for windows): `scp \*mycar\models\ pi@&lt;your_ip_address>:~/mycar/models/`
    *   
    *    Finally, start your car with the model that you just created with the command: `python manage.py drive --model ~/mycar/models/mypilot.h5.`
*   Conflicts:
    *   My first training data was only recorded for one direction in an oval track; thus, the autopilot/model could only self-drive clockwise/
        *   Reason: my initial data (image processing & control commands) only contains right steering and right-curved track since my track was an oval shape. If I trained my model using a more complex track with both-direction curves, my model wouldve been able to adapt better
*   Resolution/ Next steps:
    *   1. Change the track to a more complex path and gather data according to it.
    *   2. Use the same oval track, but gather additional data from counterclocking driving, and train a model using model data fom clockwise & counterclockwise driving.
    *   Research more about the mechanism of how multiple APIs such as Keras and Tensorflow uses neutral network to drive the car for future development.
    *   Attempt to train the model using stop signs and slow signs (need more research on how to utilize Keras and Tensorflow)

        

<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Driving-Car0.jpg). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Driving-Car0.jpg "image_tooltip")





<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/Driving-Car1.jpg). Store image on your image server and adjust path/filename if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/Driving-Car1.jpg "image_tooltip")


(All the command/actions were done on raspberry pi (car))


# 3/18/20 - Creating Car Application & Steering/Throttle Calibration



*   Notes:
    *   Created a Donkey car app/file with all default calibrations with `donkey createcar --path ~/mycar`command
    *   Ran steering and throttle channel to adjust my settings
        *   `donkey calibrate --channel &lt;your_steering_channel> --bus=1 `- Throttle calibration measurement testing
        *   `donkey calibrate --channel &lt;your_throttle_channel> --bus=1 - `Steering calibration measurement testing
        *   Set my max/Reverse max throttle value as low as possible to avoid accidental crashes
    *   Finally, to finalize and fine tune my steering calibration, I created a control webpage to control my car and measured the diameter of turns
        *   Command: `cd~/mycar`
        *   `python manage.py drive`
        *   `&lt;your car's hostname.local>:8887`
        *   Measured the diameter of the turn based on the extent of steering input
*   Conflicts:
    *   (ImportError: No module named 'numpy.testing.decorators') popped up when attempting to create a car file  (using  `donkey createcar --path ~/mycar`command).
*   Resolution:
    *   Researched on community slack channel
    *   command (pip install numpy==1.16.2) to install the compatible module
*   Next Steps:
    *   Train an autopilot
    *   Adjust the max throttle value so that the throttle becomes less insensitive


# 1/19/20 - Software Download



*   Notes:
    *   Utilizing a Donkey car guide online, installed DonkeyCar on Windows(host PC)
*   Installing Software on Donkeycar(Raspberry pi)
    *   First step: flash a micro SD image with a raspbian-stretch-lite operating system (linux) (suitable for my raspberry pi 3)
    *   raspbian-stretch-lite operating system (linux): lacks a GUI (only terminal), but instead faster & simpler for efficiently
    *    *   Other following steps: <br />
        *   Step 2: Setup the WiFi for First Boot <br />
        *   Step 3: Setup Pi's Hostname <br />
        *   Step 4: Enable SSH on Boot <br />
        *   Step 5: Connecting to the Pi <br />
        *   Step 6: Update and Upgrade <br />
        *   Step 7: Raspi-config <br />
        *   Step 8: Install Dependencies <br />
        *   Step 9: Install Optional OpenCV Dependencies <br />
        *   Step 10: Setup Virtual Env <br />
        *   Step 11: Install Donkeycar Python Code <br />
        *   Step 12: Install Optional OpenCV <br />
*   Optional Steps for better user efficiency:
    *   Utilized “PUTTY” to remotely control raspberry pi (linux environment) with host PC in order to efficiently install all configuration and programs.
    *   In order to connect: first type “`sudo raspi-config"`
    *   Then, enable “ssh”
*   Next Steps:
    *   Research more about Linux operating system & commands
    *   Create DonkeyCar application


# ---------------------------------------------------------------------


# 1/4/20 - Hardware Completion



*   Notes:
    *   Received the Servo Driver
    *   Completed Hardware Assembly by:
        *   Adding servo driver on the board
        *   Mounting wide-angle Camerica on the top of the board
        *   Mounting the board itself on top of the RC Car
        *   Detach the Throttle & steering cable from the RC Receiver
        *   Plugging int the Throttle & steering cable to channel 0 & 1 on the servo Driver
        *   Taped a separate battery for raspberry pi on top of the RC Car
        *   Finally, connect I-squared-C and power from the raspberry pi pin to the Servo driver board pin using 4 wires (power, ground, and 2 communication channels)
*   Conflicts:
    *   Battery placement:
*   Plans:
    *   Learn more about the mechanism behind connecting I-squared-C and power from the raspberry pi pin to the Servo driver board pin using 4 wires (How it works)
    *   Starting downloading the software on a host PC and on the Raspberry pi


# --------------------------------------------------------------------


# 12/26/19



*   Notes:
    *   Researched how I can use the sombrero Hat
*   Resolution:
    *   Buy a lipo battery with an xt 60 female connector
    *   Buy a charger for the battery mentioned above
    *   Sites for additional accessories that may be handy:
        *   [https://www.ebay.com/p/1840598960?iid=141113191898&chn=ps&norover=1&mkevt=1&mkrid=711-117182-37290-0&mkcid=2&itemid=141113191898&targetid=649162914607&device=m&mktype=pla&googleloc=9032152&poi=&campaignid=6470636529&mkgroupid=81597519750&rlsatarget=pla-649162914607&abcId=1140476&merchantid=101981423&gclid=Cj0KCQiA0ZHwBRCRARIsAK0Tr-ohiC4_PByu9V0boWhOFeQ68DQ7_y86lwjIJah57fJTcISXZ2sm1_AaAnb7EALw_wcB](https://www.ebay.com/p/1840598960?iid=141113191898&chn=ps&norover=1&mkevt=1&mkrid=711-117182-37290-0&mkcid=2&itemid=141113191898&targetid=649162914607&device=m&mktype=pla&googleloc=9032152&poi=&campaignid=6470636529&mkgroupid=81597519750&rlsatarget=pla-649162914607&abcId=1140476&merchantid=101981423&gclid=Cj0KCQiA0ZHwBRCRARIsAK0Tr-ohiC4_PByu9V0boWhOFeQ68DQ7_y86lwjIJah57fJTcISXZ2sm1_AaAnb7EALw_wcB)
        *   [https://www.ebay.com/p/855007662](https://www.ebay.com/p/855007662)?
        *   


# 12/25/19



*   Notes:
    *   Received the RC Car
    *   Assembled the RC Car by connecting the ESC & Battery chord and tested its performance
    *   Removed the top part of the RC Car
    *   Replaced the front and back clip with front and back 3D printed module for later assembly with 3D printed mount.
    *   Screwed the Rasberry pi board onto the 3D printed Board
    *   Xt-60: Yellow adapter
    *   Mini Tamiya: Plastic tip on RC Battery & ESC cable
*   Conflicts:
    *   Sombrero Hat:
        *   Found out that the xt 60 doesn’t directly fit with the battery & ESC outlet.
        *   Have the remove the mini Tamiya to connect it; however, then there is no way of charging the battery again with the charging cable(which has to match with the mini Tamiya)
        *   Removing/putting back the mini Tamiya to connect the battery chord to the sombrero/charging cable is very risky
*   Resolution:
    *   Ordered a Servo Driver for now
    *   Emailed the conflict through Donkey Car shopping website
*   Plans:
    *   Use the Servo Driver


# 12/21/19 - Starting of assembly



*   Notes:
    *   Received the 3D printed kit 
    *   2 different types of power/signal controller: a servo driver and a sombrero Hat
        *   Sombrero Hat:
        *   Doesn’t need an external battery
        *   First, detach the RC battery cable from ESC able
        *   After soldering the Sombrero, connect battery chord to Sombrero and ESC power chord to Sombrero
    *   Further Study Sombrero Hat
    *   Sombrero Hat requires soldering
    *   Receiving the RC Car after Christmas
*   Conflicts:
    *   Choosing whether to use Servo driver or Sombrero Hat for power/signal; a controller for Rasberry pi
        *   Servo Driver: lots of cables, ineffective, but no soldering
        *   Sombrero Hat: more efficient (no wires), but soldering.\
*   Resolution:
    *   Use Sombrero Hat for now
*   Plans:
    *   Buy a soldering kit
    *   Wait for RC Car to be delivered


# 12/20/19



*   Accomplishments: 
    *   End of final
    *   SAT score back
*   Plans:
    *   Take act diagnostic
    *   Start learning Linux and python


# 12/16/19



*   Plans: 
    *   Demo in Hwarang?


# 12/15/19



*   Plans:
    *   Create a GitHub portfolio to record my programs & progress
    *   


# 12/12/19



*   Accomplishments:
    *   Recruited 2 people who are interested in computer science for a self-driving car project 
*   Plans:
    *   Plan to start donkey car project after finals
    *   First, discuss the materials we need
    *   Learn Linux ASAP
    *   Learn Machine Learning from Coursera soon
    *   Recruit/ ask more people who want to cooperate

<!-- Docs to Markdown version 1.0β21 -->
