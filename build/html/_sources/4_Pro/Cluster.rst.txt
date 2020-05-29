==============================
Swarm
==============================

Swarm Simulation
*******************************

CopterSim also supports swarm simulations. As shown in Fig.A.18, open multiple
CopterSim programs and set the ID value of each aircraft to the desired value. Each
CopterSim needs to connect to a Pixhawk autopilot, and then click the “Start Simulation” 
button to start the HIL simulation separately. The 3D display programs (only
supports the vision developed by UE4) will automatically receive all vehicle data
from the local network and display them in the same 3D display software.

.. figure:: /images/Quan-app1-FigA.18.jpg
    :align: center

    Fig. A.18 CopterSim swarm simulation

The current distributed simulation architecture theoretically supports HIL simulation 
for any number of vehicles. The limitation mainly depends on the following
factors: the number of computer USB interfaces (each Pixhawk will occupy a USB
port), the memory size of the computer (each CopterSim will occupy a certain amount
of memory space), the computer processor speed (need to ensure that each CopterSim
can run in real-time).

Currently, CopterSim supports two methods to start the swarm simulation:

(1). The first method is to open multiple CopterSims manually. Repeat to click the
CopterSim.exe file to open an expected number of CopterSim programs one by
one, each of them assigned with a unique ID automatically . Then, connect the
serial ports and click to start the simulation.

(2). The second method is to open an expected number of CopterSim programs
together through a “bat” script, with automatically completing software configuration 
and serial port selection. Open the “CopterSim\ AutoStartScriptTemp.bat”
script with a text editor, and the following content will be observed.

* start CopterSim.exe 1 1 20100 0 0 1 0 235 0 0 4
* start CopterSim.exe 1 2 20102 0 0 1 0 235 0.5 0 5
* start CopterSim.exe 1 3 20104 0 0 1 0 235.5 0 0 6
* start CopterSim.exe 1 4 20106 0 0 1 0 235.5 1 0 7

The above code shows a Windows batch bat script that opens four CopterSim
programs at a time. As corresponding with Fig.A.19, the 0th number followed by
CopterSim.exe means “whether the simulation starts automatically”; the 1st to
9th numbers correspond to the options of the advanced functions in the CopterSim 
UI shown in Fig.A.2c; the 10th number corresponds to the Pixhawk USB
serial port number.

.. figure:: /images/Quan-app1-FigA.19.jpg
    :align: center

    Fig. A.19 Corresponding relation between CopterSim’s parameters and script’s numbers


Simulation Mode Settings
***********************************

In addition to HIL simulation, CopterSim also supports other simulation modes to
improve test efficiency. As shown in Fig.A.20, there are several types of simulation
modes supported by CopterSim.

(1). HIL simulations for different versions of PX4 firmware. Since different HIL data
interfaces are required for different PX4 firmware versions, the best matching
simulation mode needs to be selected for different PX4 firmware versions to
ensure correct and efficient HIL simulation.

(2). SIL simulation with Simulink. The swarm simulation speed is very slow if all
full dynamics models are running directly by Simulink. As a result, it is not
convenient to observe the simulation results in real-time. Therefore, readers can
convert the Simulink model into a DLL model file which can be imported to
CopterSim by the code generation method mentioned in the previous section.
Then, Simulink controller can exchange sensor data and control signals with
CopterSim programs through the UDP to form a closed-loop swarm SIL simulation 
platform. In swarm simulations, the UDP port number in Fig.A.20 needs to
be different among CopterSim programs, and then Simulink can communicate
with each CopterSim program through the corresponding port number. It should
be noted that the DLL model source code presented in Fig.A.15 also supports
to simulate a complete closed-loop system with both model and controller. This
makes it possible to directly send the speed commands to DLL models, and
perform the SIL simulations to test the top-level decision-making algorithms.

    .. figure:: /images/Quan-app1-FigA.20.jpg
        :align: center

        Fig. A.20 CopterSim simulation mode setting

(3). Connecting with the PX4 autopilot software (without Pixhawk hardware) to
perform SIL simulations on a computer. The PX4 source code also supports to
be compiled into a firmware that can be run in a computer. Run N PX4 autopilot
software on a computer, and then open N CopterSim programs to connect with
them correspondingly. Then, it is possible to perform swarm SIL simulations
with PX4 autopilot software on the same computer. Note that the PX4 software
defaults to use the TCP port 4560. [#f1]_ Readers can manually specify the port number
in the PX4 startup script to match with the CopterSim programs.


Multi-computer Distributed Simulation
******************************************
As mentioned in the previous section, the computing performance and memory space
of a single computer are limited, so it is impossible to support swarm simulation for
an unlimited amount of vehicles. Therefore, CopterSim also provides the function to
perform distributed simulation through Local Area Network (LAN) by using multiple
computers. As shown in Fig.A.21, enable the “Link” option on the UI of CopterSim 
to start the network broadcast function. The flight data of each CopterSim will
be received by all computers via the LAN. Therefore, with enough computers connecting 
to the LAN, and a certain amount of CopterSim programs (in HIL or SIL
simulation modes) are run on each computer, the platform can realize swarm distributed 
simulation for any number of vehicles. At the same time, each computer can
open multiple 3D scene programs to observe all vehicles from multiple perspectives.
Note that if the “Link” checkbox is unchecked, the flight information of CopterSim
can only be received by this computer, so it will not affect other computers, which
is more suitable for the use in experimental courses.

.. figure:: /images/Quan-app1-FigA.21.jpg
    :align: center

    Fig. A.21 CopterSim distributed simulation architecture



Swarm Control in Simulink
************************************************

For swarm simulation, communication and real-time control is a difficult task. In
response to these needs, we have developed tutorials with source codes (see Fig.A.22)
based on the advanced functions of this experimental platform. The main implemented 
features are shown in the following.

.. figure:: /images/Quan-app1-FigA.22.jpg
    :align: center

    Fig. A.22 Source code for Simulink swarm control

(1). Open-loop Swarm SIL simulation. The advanced platform can send swarm data
to the UE4 scene display software with the Simulink UDP interface to preview
the trajectories of all vehicles. With this function, on the one hand, it is convenient
to generate trajectories for static or moving obstacles, so complex swarm flight
scenes can be visualized as shown in Fig.A.23. On the other hand, it provides the
opportunity to preview the swarm flight performance, which helps developers to
improve the designed trajectories.

    .. figure:: /images/Quan-app1-FigA.23.jpg
        :align: center

        Fig. A.23 Example for heterogeneous unmanned systems in UE4

(2). Closed-loop Swarm SIL simulation. The advanced platform provides a Simulink
UDP interface to exchange motion states and control signals from all CopterSim 
SIL control models to realize the closed-loop swarm SIL simulation. The
CopterSim SIL control model can be 1) a DLL model file including both a multicopter 
motion model and a velocity-loop controller; or 2) CopterSim motion
model controlled by a PX4 autopilot under the SIL simulation mode.

(3). Closed-loop Swarm HIL simulation. The advanced platform provides a Simulink
UDP interface to exchange motion states and control signals from all CopterSim
HIL control models to realize the swarm HIL simulation. The CopterSim HIL
control model is a closed-loop control system involving real Pixhawk autopilots. 
CopterSim can automatically forward Mavlink message packets from the
Pixhawk autopilot serial port to Simulink. Furthermore, interfaces are also 
developed to directly encode and decode Mavlink message in Simulink. As a result,
users can control each Pixhawk+CopterSim HIL system by Simulink.

(4). Closed-loop swarm flight by Simulink. The advanced platform provides the serial
communication interface to directly exchange data with each Pixhawk autopilot
via wireless radio telemetry, as well as UDP/ROS interfaces to communicate
with vehicles in the same WIFI network. Therefore, it is convenient to realize the
functions of GCSs to receive flight data from multiple vehicles in real-time and
send back control signals. Compared with GCS software developed by C/C++, it
is more convenient to tune the controller parameters on line and observe the realtime 
control performance in Simulink. Besides, the Simulink swarm controller
can also be converted into C/C++ to improve the running speed.

Through the above procedure, developers can perform the development, simulations
and flight tests in a step-by-step process, which may significantly improve the development 
efficiency for swarm control systems.


.. rubric:: Reference
.. [#f1] http://dev.px4.io/master/en/simulation/