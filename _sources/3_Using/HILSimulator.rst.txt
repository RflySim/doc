=========================
HIL Simulation Platform
=========================

The HIL simulation platform includes a Real-time Motion Simulation Software—
CopterSim and a 3D Visual Display Software—3DDisplay.



CopterSim
-------------------------

Double-click the CopterSim shortcut on the Windows desktop to open the CopterSim 
software, whose UI is presented in Fig. 3.50. The default simulation model and
parameters are the same as for the Simulink multicopter model used in the SIL 
simulation system (see Fig. 3.1). This is because the CopterSim is developed based on 
the code generation technique with the Simulink multicopter model. CopterSim needs
to run on a 64-bit Windows computer platform with a serial port and a MicroUSB
cable to communicate with the Pixhawk autopilot (see Fig. 3.42).

.. figure:: /images/Quan-ch3-Fig3.50.jpg
    :align: center

    Fig. 3.50 CopterSim main UI

CopterSim sends sensor data to the Pixhawk autopilot, and then the autopilot
solves the motor PWM control signal and returns it to CopterSim. As a result, the
Pixhawk autopilot can perform real-time control on the simulated multicopter in
CopterSim, as well as control a real multicopter. Meanwhile, CopterSim will send
the attitude and position information of the multicopter to the local network through
the UDP protocol, and the 3DDisplay receives the multicopter flight information to
complete the corresponding real-time 3D scene display.

As shown in Fig. 3.50, the UI of CopterSim is divided into two parts. The upper
part, presented in Fig. 3.50a, is the input interface to design a multicopter by selecting
popular components on the market. The lower part presented in Figs. 3.50b–e is the
interface to connect with the autopilot for HIL simulation. Note that CopterSim
enables by default only the basic functions required by this book. Registration is
required to use many other practical functions, such as swarm simulation, high-
fidelity UE4 scenes, and HIL simulations for other aerial vehicles (e.g., fixed-wing
aircraft). Please, see Appendix A for more information.

Click the “Model Parameter” button in the middle of the CopterSim UI in
Fig. 3.50b. The model parameter configuration dialog in Fig. 3.51 will pop up; the
model parameters stored in the previous simulation will be displayed here. The
parameter dialog in Fig. 3.51 mainly includes two parts: the hover information (hover
endurance, throttle, output power, motor speed, etc.) and the basic multicopter 
parameters (total mass, the moment of inertia, size, thrust coefficient, and drag coefficient).
Clicking the “Restore to Default Params” button on the dialog in Fig. 3.51 will restore
the model parameters to the default values; clicking the “Save and Apply Params”
button will store the current parameters to the database for subsequent HIL simulations.

.. figure:: /images/Quan-ch3-Fig3.51.jpg
    :align: center

    Fig. 3.51 Model parameter configuration dialog

CopterSim also allows readers to directly modify the model parameters on the
right page of Fig. 3.51. For example, enter the same parameters as the multicopter 
model used in Simulink SIL simulations (the parameters are stored in file
“e0\1.SoftwareSimExps\icon\Init.m”). Then, click the “Store and Apply parameters” 
button in Fig. 3.51 to store and apply the model parameters. The “noise level
(0–1)” in Fig. 3.51 allows selecting the noise level of the simulated sensors, where
“0” denotes that the sensor noise is not enabled, and “1” denotes that the noise level
is consistent with the real Pixhawk autopilot. A noise level between 0–1 or larger
than one can also be selected to represent the noise level of actual sensors. This
enables the possibility of testing the anti-interference ability of the designed control
algorithms.

After the multicopter parameters and the noise level are configured, as shown in
Fig. 3.51, connect the Pixhawk autopilot with the computer. A few seconds later, the
serial port of the Pixhawk autopilot will be listed in the “Select Pixhawk Com” 
dropdown menu. Select the Pixhawk serial port (usually described by the text “FMU”),
and click the “Start Simulation” button to start the HIL simulation. As shown in
Fig. 3.52, the messages from the Pixhawk are printed on the CopterSim UI, which
indicates that the HIL simulation is running correctly. During the HIL simulation
process, clicking the “Stop Simulation” button will stop the HIL simulation, and
clicking the “Restart Simulation” will re-initialize the multicopter position and states
to their initial values.

.. figure:: /images/Quan-ch3-Fig3.52.jpg
    :align: center

    Fig. 3.52 HIL simulation with CopterSim



3DDisplay
--------------------------

Double-click the 3DDisplay shortcut on the Windows desktop to open the 3DDisplay
software. As shown in Fig. 3.53, the “3D Scene Viewer” on the left side of the
3DDisplay UI presents the current flight status of the multicopter in the 3D scene.
The basic flight parameters are displayed in the upper right window of the 3DDisplay
UI, including motor speed, position, and attitude information. The flight trajectory
of the multicopter is displayed on the lower right window of the 3DDisplay UI.

.. figure:: /images/Quan-ch3-Fig3.53.jpg
    :align: center

    Fig. 3.53 User interface of 3DDisplay



Flight Tests with HIL Simulation Platform
--------------------------------------------

In the HIL simulation platform, when controlling a real multicopter, it is convenient
to control the simulated multicopter with a real RC transmitter to perform basic
actions, such as arming, taking off, manual flight, landing, etc. The detailed steps are
described next.

(1). Push up the POWER switch to turn on the RC transmitter.

(2). Correctly connect the computer with the Pixhawk hardware system (including
the Pixhawk autopilot and the RC receiver) and start the HIL simulation in
CopterSim according to the procedure mentioned above.

(3). As shown in Fig. 3.54a, arm the Pixhawk autopilot by moving the left-hand
stick on the RC transmitter (CH3) to the lower-right corner for 2–3 s.

    .. figure:: /images/Quan-ch3-Fig3.54.jpg
        :align: center

        Fig. 3.54 Arm and disarm of Pixhawk autopilot through RC transmitter

(4). Pixhawk is successfully armed when its LED turns from slow flashing to always
on, [#f1]_ and the CopterSim print message “Detect Px4 Armed” is received from
Pixhawk. If arming Pixhawk fails, please disconnect all hardware and software
and repeat the above steps.

(5). Pull up the left-hand stick on the RC transmitter (CH3) for the multicopter to
take off and fly up to a certain altitude. Next, vertically move the left-hand stick
to verify the vertical motion control of the multicopter.

(6). Horizontally move the left-hand stick on the RC transmitter (CH4) to verify
the yaw angle motion control of the multicopter.

(7). Vertically move the right-hand stick on the RC transmitter (CH2) to verify the
pitch angle control as well as the forward and backward motion control of the
multicopter.

(8). Horizontally move the right-hand stick on the RC transmitter (CH1) to verify the
roll angle control as well as the left and right motion control of the multicopter.

(9). Change the position of the top-right switch on the RC transmitter (CH6) to
verify the mode switching control of the multicopter.

(10). Pull down the left-hand stick on the RC transmitter (CH3) to land the 
multicopter to ground.

(11). As shown in Fig. 3.54b, move the left-hand stick on the RC transmitter (CH3)
to the lower-left corner for 2–3 s to disarm the Pixhawk.

(12). Click the “Stop Simulation” button on the CopterSim UI to stop the HIL 
simulation. Then, disconnect all software and hardware connections between the
computer and Pixhawk.


.. rubric:: Notes
.. [#f1] Higher Pixhawk hardware (e.g., Pixhawk 2/3/4/5) starts to discard LED module, so an external I2C LED module is required to observe the lighting effect.