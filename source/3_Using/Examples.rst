Examples 
==========================================

Experimental Procedure for LED Control Experiment
--------------------------------------------------

The flashing frequency and color of the LED on the Pixhawk hardware can be controlled 
by designing controller in Simulink. This section takes a simple LED light
control experiment [#f1]_ as an example to introduce the operation process of the hardware
and software components of the experimental platform released with this book.

Experimental Objective
*********************************

As shown in Fig. 3.54, use two channels from CH1 to CH5 of the RC transmitter to
control the LED light on Pixhawk in two different colors and two different modes.

.. figure:: /images/Quan-ch4-Fig4.2.jpg
    :align: center

    Fig. 3.54 Hardware connection of LED control experiment


Experimental Procedure
*********************************

The experiment uses the “RGB_LED” module in the PSP toolbox introduced in the
previous chapter (see Fig. 3.55) to control the LED light on Pixhawk.

(1). Create and open a new Simulink model file. As shown in Fig. 3.55, find the
“RGB_LED” module in the “Pixhawk Target Blocks” toolbox, which is in the
“Library Browser” of Simulink, and drag it to the new created Simulink file. The
RC transmitter module “input_rc” in Fig. 3.55 is also dragged into the Simulink
as the input signals to control the LED light. A Simulink example file completing 
the whole process of configuration is available in “e0\2.PSPOfficialExps\px4demo_input_rc.slx”.

.. figure:: /images/Quan-ch4-Fig4.3.jpg
    :align: center

    Fig. 3.55 LED output interface model for PSP toolbox

(2). The RBG_LED module can be used to control the mode and color of the LED
light on Pixhawk. Its mode enumeration variable “RGBLED_MODE_ENUM”
includes the following seven options

* SL MODE OFF
* SL MODE ON
* SL MODE DISABLED
* SL MODE BLINK SLOW
* SL MODE BLINK NORMAL
* SL MODE BLINK FAST
* SL MODE BREATHE.

The color variable “RGBLED_COLOR_ENUM” has the following options

* SL COLOR OFF
* SL COLOR RED
* SL COLOR GREEN
* SL COLOR BLUE
* SL COLOR YELLOW
* SL COLOR PURPLE
* SL COLOR AMBER
* SL COLOR CYAN
* SL COLOR WHITE.

The above variables have been registered as MATLAB global parameters when
installing the PSP toolbox so that they can be directly applied. For example,
an LED light with blue color and fast blinking mode can be obtained by sending 
the variable “RGBLED_MODE_ENUM.SL_MODE_BLINK_FAST” with
the “Constant” module to the “Mode” port of the LED module (the upper
input port of the LED module), and sending the variable “RGBLED_COLOR_ENUM.SL_COLOR_BLUE” 
with the “Constant” module to the “Color” port
(the lower input port of the LED module).

(3). Controller design. According to the introduction to the RC system provided in
the previous chapter, the data range of the PWM signals received by Pixhawk is
1100–1900. As shown in Fig. 3.56, we will use two channels of the RC transmitter
in this experiment to control the mode and color of the LED light. The controller
design procedure is described next.

    .. figure:: /images/Quan-ch4-Fig4.4.jpg
        :align: center

        Fig. 3.56 LED controller with an RC transmitter

    1). Use the CH3 channel of the RC transmitter (see the throttle channel in
    Fig. 3.54) to change the blink mode of the LED light. When the throttle stick
    is turned to the upper side, i.e., when the PWM value of the CH3 channel is 
    higher than 1500 microseconds (abbreviated as CH3>1500), then the
    “Mode” port receives an “RGBLED_MODE_ENUM.SL_MODE_BLINK_FAST” 
    variable corresponding to a fast blinking mode; when CH3≤1500, the
    “Mode” port receives the “RGBLED_MODE_ENUM.SL_MODE_BLINK_NORMAL” 
    variable corresponding to a slow blinking mode.

    2). Use the CH4 channel of the RC transmitter to change the color of the LED
    light. When CH4>1500, the “Color” port receives an “RGBLED_COLOR_ENUM.COLOR_RED” 
    variable corresponding to red color; when
    CH4≤1500, the “Color” port receives an “RGBLED_COLOR_ENUM.
    COLOR_BLUE” variable corresponding to blue color.


Controller Code Generation and Firmware Uploading
******************************************************

(1). For MATLAB 2017b–2019a, as shown in Fig. 3.57, click the “Simulation”—“Model 
Configuration Parameters” option on the Simulink menu bar to enter the
Simulink setting dialog; for MATLAB 2019b and above, click the “Settings”
button. The obtained Simulink setting window is presented in Fig. 3.58.

.. figure:: /images/Quan-ch4-Fig4.5.jpg
    :align: center

    Fig. 3.57 “Model Configuration parameters” option on Simulink

.. figure:: /images/Quan-ch4-Fig4.6.jpg
    :align: center

    Fig. 3.58 Simulink setting dialog

(2). Select the target hardware. As shown in Fig. 3.59, set the option “Hardware
Implementation”—“Hardware Board” to “Pixhawk PX4”.

.. figure:: /images/Quan-ch4-Fig4.7.jpg
    :align: center

    Fig. 3.59 Setting target hardware to Pixhawk PX4

(3). Compile the model. As shown in Fig. 3.60, compile the designed controller into
the PX4 firmware file by clicking the “Build” button on the Simulink toolbar.
The code generation and firmware compiling process can be observed in the
“Diagnostic Viewer” window of Simulink.

.. figure:: /images/Quan-ch4-Fig4.8.jpg
    :align: center

    Fig. 3.60 Button for compiling code in Simulink

For MATLAB 2017b–2019a, it can
be opened by clicking on the “View diagnostics” button in the status bar below
Simulink (see the lower box in Fig. 3.61) or by clicking the “View” - “Diagnostic
Viewer” (see Fig. 3.61) button on the Simulink menu. For MATLAB 2019b and
above, click the “Diagnostics” button to open the “Diagnostic Viewer” window.

.. figure:: /images/Quan-ch4-Fig4.9.jpg
    :align: center

    Fig. 3.61 “Diagnostics” option in different Simulink versions

As shown in Fig. 3.62, the code and firmware are compiled successfully when
the “Build process completed successfully” message appears in the “Diagnostic 
Viewer” window. A code generation report shown in Fig. 3.63 can also be
obtained. At this point, the corresponding C/C++ code files have been generated 
in the folder “Firmware\src\modules\px4_simulink_app”, and the “make
px4fmu-v3_default” command has been called to complete the firmware compilation process.

.. figure:: /images/Quan-ch4-Fig4.10.jpg
    :align: center

    Fig. 3.62 Diagnostic viewer showing “build process completed successfully”

.. figure:: /images/Quan-ch4-Fig4.11.jpg
    :align: center

    Fig. 3.63 Generated report after compiling

(4). Upload the firmware. Use the one-key upload function provided by the PSP
toolbox to upload the PX4 firmware file. The specific steps are presented as
follows.

    1). Connect the MicroUSB port of the Pixhawk hardware with the computer by
    using a USB cable.

    2). For MATLAB 2017b–2019a, as shown in Fig. 3.64, click the “Code”-“PX4
    PSP: Upload code to Px4FMU” in the Simulink menu bar; for MATLAB 2019b and 
    above, input the “PX4Upload” command in the MATLAB
    “Command Window” according to Fig. 3.40b to upload the firmware.

    .. figure:: /images/Quan-ch4-Fig4.12.jpg
        :align: center

        Fig. 3.64 Simulink firmware upload menu

    3). As shown in Fig. 3.65, Simulink will automatically recognize the Pixhawk
    autopilot and start to upload and deploy the PX4 firmware file. The 
    uploading and deploying process is successfully completed when the progress bar
    reaches 100%. Note that Pixhawk may need to be re-plugged in some cases
    to start the upload progress.

    .. figure:: /images/Quan-ch4-Fig4.13.jpg
        :align: center

        Fig. 3.65 Firmware is successfully uploaded


Experimental Result
*********************************

By default, when the RC transmitter does nothing, the LED light is slowly blinking in
blue. As shown in Fig. 3.66, do the following steps to verify the experimental results.

(1). When the left-hand stick of the RC transmitter shown in Fig. 3.54 is placed in the
upper-right position (CH3>1500 and CH4>1500), the LED light on Pixhawk
is quickly blinking in blue.

(2). When the throttle stick of the RC transmitter is placed in the upper-left position
(CH3>1500 and CH4<1500), the LED is quickly blinking in red.

(3). When the throttle stick of the RC transmitter is placed in the lower-left position
(CH3<1500 and CH4<1500), the LED is slowly blinking in red.

(4). When the throttle stick of the RC transmitter is placed in the lower-right position
(CH3<1500 and CH4>1500), the LED is slowly blinking in blue.

.. figure:: /images/Quan-ch4-Fig4.14.jpg
    :align: center

    Fig. 3.66 LED experimental results (the left LED is blue, and the right is red)



Experimental Procedure of Attitude Control Experiment
--------------------------------------------------------

This section uses a well-designed attitude control system as an example to introduce
the basic operation process of all the controller design experiments. This example is
certainly complicated than the previous LED light control experiment.


Simulink-Based Algorithm Design and SIL Simulation
******************************************************

(1). **Step 1** : controller design

Create a new Simulink file and design a multicopter attitude controller in it.
For simplicity, an example of a well-designed attitude controller is available
in “e0\3.DesignExp\Exp_AttitudeController.slx”. Open it, and the controller
details are presented in Fig. 3.67. The design requirements for the controller are
in the following.

    .. figure:: /images/Quan-ch4-Fig4.15.jpg
        :align: center

        Fig. 3.67 Attitude controller example

    1). Input data

    * CH1-CH5 channel signals of the RC transmitter (see Fig. 3.67), which correspond to the “ch1”-“ch5” input ports in Fig. 3.67. The actual data approximately range from 1100 to 1900, so calibration or dead zones are required in processing the RC data.
    * Multicopter angular velocity (corresponding to the “p”, “q”, “r” input ports in Fig. 3.67, unit: rad/s). The above three inputs represent the velocity rotating around the x-axis of the body, the velocity rotating around the y-axis of the body, and the velocity rotating along the z-axis of the body.
    * Multicopter Euler angles (unit: rad). Here, the roll angle and the pitch angle (corresponding to the “roll” and “pitch” input ports in Fig. 3.67) are mainly considered, and the yaw control is temporarily not considered in this experiment.

    2). Output data

    * PWM control signals of four motors (corresponding to the “PWM” output port in Fig. 3.67). The data range is 1000–2000.
    * Identifier for the armed state (corresponding to the “ARM_Control” output port in Fig. 3.67). The data type is Boolean.

    3). Expected effects

    * The throttle stick (CH3 on the RC transmitter) controls multicopters to perform the upward-and-downward movement.
    * Push up the pitch stick (CH2 < 1500) to control the multicopter flying forward.
    * Move the roll stick leftward (CH1 < 1500) to control the multicopter flying leftward.
    * Pull back (or down) the three-position switch (CH5 > 1500) to disarm the multicopter.

(2). **Step 2** : generate the controller subsystem

Select all the components in Fig. 3.67 with the mouse (or simultaneously press
the keys CTRL + A), and right-click the mouse, choosing “Create Subsystem
From Selection” to pack the controller to a subsystem in Simulink. Right-click
the obtained subsystem and click “Mask”—“Create Mask” to open the mask
setting box in Fig. 3.68. Then, enter text “image(‘./icon/Pixhawk.png’);” in the
“Icon drawing commands” input box in Fig. 3.68. Finally, click the “OK” button
and adjust the positions of the input and output ports of the obtained subsystem
to get a subsystem as presented in Fig. 3.69.

.. figure:: /images/Quan-ch4-Fig4.16.jpg
    :align: center

    Fig. 3.68 Mask setting dialog for Simulink subsystem

.. figure:: /images/Quan-ch4-Fig4.17.jpg
    :align: center

    Fig. 3.69 Obtained attitude controller subsystem

(3). **Step 3** : integrate the controller with the model

Open the Simulink file for SIL simulation, i.e., file 
“e0\1.SoftwareSimExps\CopterSim3DEnvironment.slx” used in the previous chapter; 
delete its original controller subsystem (remember to create a backup); then, 
copy the new controller subsystem obtained in **Step 2** to replace it.

(4). **Step 4** : connect and configure the inputs and outputs

As shown in Fig. 3.70, reconnect the controller to the multicopter model, where
the output port “PosE” denotes the multicopter position vector in the earth
frame, “AngEuler” denotes the Euler angle vector of the multicopter attitude,
and “AngRateB” denotes the angular velocity vector of the multicopter. Given
that the RC transmitter signals cannot be obtained in the SIL simulation phase,
readers can use constant values to replace them or use the MATLAB functions to simulate 
the corresponding RC transmitter actions. The angular velocity
input ports “p”, “q”, and “r” of the controller in Fig. 3.69 can be obtained from
the “AngRateB” vector of the multicopter model; the angle “roll” and “pitch”
can be obtained from the “AngEuler” vector. An example is also available in
“e0\3.DesignExps\Exp2_ControlSystemDemo.slx” whose controller and practical RC 
transmitter signals have been connected as presented in Fig. 3.70.

.. figure:: /images/Quan-ch4-Fig4.18.jpg
    :align: center

    Fig. 3.70 Controller connected with multicopter model

(5). **Step 5** : start a joint simulation

Click the FlightGear-F450 shortcut on the Windows desktop to open FlightGear,
and click on the “Start Simulation” button on the Simulink UI to start the simulation. 
Then, it can be observed in FlightGear (see Fig. 3.71) that a quadcopter
climbs up for some time and then rolls left and flies leftward, indicating that the
controller has achieved the expected requirements.

.. figure:: /images/Quan-ch4-Fig4.19.jpg
    :align: center

    Fig. 3.71 A quadcopter in FlightGear



Code Generation and Configuration
**********************************

(6). **Step 6** : configuration of the code generation environment

After finishing the SIL simulation in Simulink, copy the obtained controller
subsystem to file “e0\3.DesignExps\Exp3_BlankTemp.slx” (this file has been
configured with all the settings required for code generation). Readers can also
create a blank Simulink file and configure it according to Fig. 3.59.

(7). **Step 7** : connect the controller to the PSP modules

Extract the corresponding I/O interfaces from the Simulink PSP module library
(see Fig. 3.55) and connect it to the controller obtained in Step 6. As shown
in Fig. 3.72, a complete example is available in “e0\3.DesignExps\Exp4_AttitudeSystemCodeGen.slx”. 
Note that the motor control signals should be
sent the uORB message of “actuator_outputs” to the “uORB Write” module
instead of the PWM output module. This is because the controller is currently
used for HIL simulation instead of actual flight tests.

.. figure:: /images/Quan-ch4-Fig4.20.jpg
    :align: center

    Fig. 3.72 Attitude controller in Simulink for code generation

(8). **Step 8** : generate code and compile the firmware

Click the “Build” button (see Fig. 3.37) on the Simulink toolbar to automatically
generate code and PX4 firmware file. The result in Fig. 3.73 shows a successful
compilation process.

.. figure:: /images/Quan-ch4-Fig4.21.jpg
    :align: center

    Fig. 3.73 Simulink controller compiling successfully

(9). **Step 9** : upload the firmware

Connect the computer to the Pixhawk autopilot with a USB cable, then use the
“PX4Upload” function (see Fig. 3.40) to upload the firmware to the Pixhawk. A
successful uploading result is shown in Fig. 3.74.

.. figure:: /images/Quan-ch4-Fig4.22.jpg
    :align: center

    Fig. 3.74 Upload firmware successfully



HIL Simulation
*******************************

(10). **Step 10** : hardware system connection

As shown in Fig. 3.54, connect the RC receiver to Pixhawk with a three-color
JR cable, then connect Pixhawk to the computer via a USB cable. At this point,
readers can observe that the LED on Pixhawk lights up and blinks slowly, [#f2]_ the
LED on the RC receiver is blue and white (this is for RadioLink and green light
for Futaba receiver). Then, turn on the RC transmitter, readers can observe that
the LED light on the Pixhawk blinks quickly for a few seconds, indicating that
the RC transmitter data has been successfully received. If there is no change
for the Pixhawk LED light, indicating that the connection between the RC
transmitter and the receiver is not correct, readers should check and confirm
the hardware connection.

(11). **Step 11** : CopterSim configuration

Double-click the CopterSim shortcut on the Windows desktop to open it. There
is no need to change the model parameters (or click “Model Parameters” -
“Restore Default Parameters” - “Storage and Use Parameters” to restore aerial
vehicle parameters to default values). Select the serial port of the Pixhawk
autopilot in the “Select Pixhawk Com” drop-down box (usually in the format
“`*** FMU COM*`”), click the “Start Simulation” button to start HIL simulation.
As shown in Fig. 3.75, the message returned by the Pixhawk autopilot will be
printed on the lower-left box of the CopterSim UI.

.. figure:: /images/Quan-ch4-Fig4.23.jpg
    :align: center

    Fig. 3.75 Model simulator software configuration in CopterSim

(12). **Step 12** : 3DDisplay configuration

Double-click the 3DDisplay shortcut on the desktop to open it. This software
does not require any configuration; it passively receives the flight attitude and
trajectory information of multicopters sent by CopterSim and displays it in
real-time. The multicopter can be controlled by the RC transmitter to verify
the designed attitude control algorithm. Move the throttle stick on the RC
transmitter to the lower-right corner for three seconds to disarm the Pixhawk,
and pull down (or back) the CH5 stick to the rearming position to disarm the
designed controller. Then, the RC transmitter is able to control the multicopter
to complete the corresponding action. As shown in Fig. 3.76, the multicopter
attitude and position can be observed on the left side of the 3DDisplay interface.
The real-time flight data are observed in the upper-right region, whereas the
multicopter trajectory is observed in the lower-right region of the 3DDisplay UI.

.. figure:: /images/Quan-ch4-Fig4.24.jpg
    :align: center

    Fig. 3.76 Multicopter 3DDisplay interface



Flight Test
**************************************

(13). **Step 13** : mount Pixhawk onto a multicopter airframe

The multicopter used in the outdoor flight tests is an F450 quadcopter (see
Fig. 3.77). The parameters of the multicopter are accurately measured and
identified by the system identification methods to ensure that the multicopter
simulation model is consistent with the dynamics of the real multicopter system. 
For outdoor flight tests, the airframe of Pixhawk should be changed from
“HIL Quadcopter X” to “DJI Flame Wheel F450” in QGC, which is presented
in Fig. 3.78. All sensors should also be calibrated in QGC.

.. figure:: /images/Quan-ch4-Fig4.25.jpg
    :align: center

    Fig. 3.77 F450 airframe and its components

.. figure:: /images/Quan-ch4-Fig4.26.jpg
    :align: center

    Fig. 3.78 Flight test airframe in QGC

(14). **Step 14** : modify the Simulink controller

Open the Simulink file in Fig. 3.72 and change the “uORB Write” module to
the “PWM_out” module provided by the PSP toolbox, according to Fig. 3.79.
An example with the modified motor output is presented in “e0\3.DesignExps\
Exp5_AttitudeSystemCodeGenRealFlight.slx”. Then, click the Simulink
“compile” button to compile the controller into PX4 firmware and upload it to
Pixhawk.

.. figure:: /images/Quan-ch4-Fig4.27.jpg
    :align: center

    Fig. 3.79 Changing “uORB Write” module to PWM_output

(15). **Step 15** : preparation for flight tests

Owing to the lack of complete failsafe logic for the generated control algorithm,
safety should be fully considered to prevent accidents in outdoor flight tests.
For example, the tests should be carried out in a relatively open area (such as
a lawn) and on a nice day with good weather and low wind speed. When the
above conditions are met, connect Pixhawk with the battery, and press the safety
switch [#f3]_ on Pixhawk for more than three seconds. Then, control the multicopter
with an RC transmitter to verify the actual performance of the controller.

(16). **Step 16** : test results and analysis

Next, we will present the results from the HIL simulation and outdoor flight
tests to verify the accuracy of the multicopter simulation model. Figure 3.80
presents the HIL simulation results when the sensor noise level in CopterSim
is set to 1.0, where the solid line “PitchReal” represents the outdoor flight
tests result, the dotted line “PitchSim” represents the simulation result, and the
dashed line “PitchSP” represents the ideal expected value. It can be observed
from Fig. 3.80 that the step response curves from the HIL simulation and the
outdoor flight are close to each other in terms of dynamic processes and noise
levels.

.. figure:: /images/Quan-ch4-Fig4.28.jpg
    :align: center

    Fig. 3.80 HIL simulation result when noise level is set to 1.0

Figure 3.81 is the HIL simulation result when the noise level in CopterSim is set
to 0. It can be seen that the response curve of the HIL simulation is very smooth with
no noise disturbance, and the dynamic process and outdoor flight results are slightly
different. Note that because the airframe “HIL Quadcopter X” is not exactly the same
as the airframe “DJI Flame Wheel F450” used in outdoor flight, there are differences
in the controller parameters. In addition, the data transmission speed of the Pixhawk
serial port may fluctuate during the HIL simulation, thereby affectingthe real-time
performance. Finally, the aerodynamics of the multicopter in the outdoor flight is
very complicated, but a simplified aerodynamic model is used in the multicopter
simulation model. Therefore, the error between their response curves is acceptable.

.. figure:: /images/Quan-ch4-Fig4.29.jpg
    :align: center

    Fig. 3.81 HIL simulation result when noise level is set to 0



.. rubric:: Notes
.. [#f1] Higher Pixhawk hardware (e.g., Pixhawk 2/3/4/5) starts to discard LED module, so an external I2C LED module is required to observe the experiment result.
.. [#f2] Higher Pixhawk hardware (e.g., Pixhawk 2/3/4/5) starts to discard LED module, so an external I2C LED module is required to observe the lighting effect.
.. [#f3] https://docs.px4.io/master/en/config/airframe.html#safety_switch