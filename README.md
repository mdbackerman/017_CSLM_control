# <em>Please see [this new repository](https://github.com/Orzel017/017_CSLM_control). This repository has moved!</em>



### 017_CSLM_control

About: ISEC room 017 CSLM control software

#### Dates:

102822 $\rightarrow{}$ 110322

#### Old text from b00_gui:

Dates: 102822 -> 112222

Author: Miles D. Ackerman (undergraduate during the summer of 2022). Email: miles.ackerman1@gmail.com

General info:
This file makes a GUI to control the room-temp NV center-based measurement setup in LISE room B00 in the Lukin Group in the Harvard PHY dept. The setup
is a confocal laser scanning microscope. A galvo steers a laser beam at 518 nm (butteryfly) through a 4F telescope setup. An excitation and a collection
path (both use fiber coupling) are present. The sample stage is manually-controlled by positioning dials. Additionally, the z-axis of the microscope
objective is controlled by a piezo. This entire setup is controlled by a NI-cDAQ (model 9147). The NI-DAQmx is the National Insturments API that is 
used to communicate with the cDAQ device. Info. about this device can be found at:
https://nidaqmx-python.readthedocs.io/en/latest/https://nidaqmx-python.readthedocs.io/en/latest/. Two cards/modules are present in the cDAQ chassis: 1.
NI-9402 (four bi-directional digital input/output (I/O) channels -also featuring programmable internal clocks for counting). Info about the NI-9402 
module can be found at: https://www.ni.com/en-us/support/model.ni-9402.htmlhttps://www.ni.com/en-us/support/model.ni-9402.html. This module functions 
as a counter based on an internal clock within the module. The parameters for creating a counter assigned to this module when it is created in each 
scanning script. The counter requires the use of two of the four available channels on this cDAQ card. One channel is for input (from the APD on the
optical bench), and one channel for the hardware-timed clock to "run" the counter. Currently (as of 081522) only one counter (analog input) channel 
can be created at a time. In order to change this functionality, the source code for this contributed drivers package must be edited. And 2. NI-9263 
(four analog output channels (-10 V to +10 V). This module's info can be found at: 
https://www.ni.com/en-us/support/model.ni-9263.htmlhttps://www.ni.com/en-us/support/model.ni-9263.html. This moduel is used for programmable digital 
output. This functionality is largely used for controlling the servo motors on the ThorLab's galvo (by writing a sequence of voltages to them). Here,
all available digital output channels are created in one line: `ni_9263_ao_channels` where a single channel can be accessed at a time. The main 
function of this application is running confocal scannign scripts in different planes (the XY plane at a specified Z height, the XZ plane across a 
specified z-range, and the YZ plane at a specified X range). The GUI is split into 2 main setions, a left-half and a right-half section. The left-hand 
section contains the input controls for running a specific scanning script. On the bottom of the left-hand section is an option to save the dataset 
that was just scan and plotted on the right. Additionally, a text output box is present at the bottom of the left_window section. This is where the 
user-entered scanning parameters are printed to. Here, the use ahs the option to select and then copy the scan parameter info for keeping a record. 
there is also the option (currently commented out) to print this same info w/ its same format to the terminal. The right-hand section conatins the 
output plot from a run scan. Include info more: this application impements live plotting for each scanning option.

For the user of this application:
1. This application was built within a virtual environment on this computer called: "NV_control" it can be found through the
user/miniconda3/envs/NV_control. Within this enviornment THIS file and additonal referenec packages can be found
2. Only limited input-validation/error checking has been implemented so far. Please be advised when running scanning programs. The LIMIT of the voltage 
that can be driven to either mirror (or the objective's z_piezo) is 10 V. DO NOT EXCEED THIS VALUE. The system (as a cause of NI-DAQmx error 
checking) will likely refuse such a request, but it is best practice to avoid.

Helpful info. when reading through this application code:
1. The NI-cDAQ card (chasis) is called (this can be changed using the NI-MAX software when the NI-DAQ card is connected to this computer)
"cDAQ1". Additional info. about the cDAQ device and its inserted modules (as of 081522 only ni_9402 and ni_9263) can be viewed in the NI-MAX software.
This software opens automatically when the cDAQ device is connected to this computer
2. The first module inserted into the cDAQ card (the NI-9402 module) is called "mod1". This naming pattern follows the available slots within the 
cDAQ chasis (there are four available slots)
3. The second module in the cDAQ chasis (the NI-9263 module) is called "mod2" following in suit

## New info

Text here
