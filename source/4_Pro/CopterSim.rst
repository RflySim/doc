====================================
CopterSim
====================================

Registration Method of CopterSim
-----------------------------------

The registration method is presented as follows.

(1). As shown in Fig.A.1, click the “Activate” button in the middle of the CopterSim
UI, and an activation dialog will pop up.

(2). Click the “Copy Hardware ID” button to copy the Hardware ID, then visit https://
flyeval.com/course and follow the steps to get the serial number and additional
software package.

(3). Paste the serial number into the “Serial Num” input box shown in Fig.A.1, and
click the “Activate” button to register CopterSim.


.. figure:: /images/Quan-app1-FigA.1.jpg
    :align: center

    Fig. A.1 CopterSim registration dialog

As shown in Fig.A.2, the complete UI of CopterSim after registration is mainly
divided into five parts. FigureA.2a is the interface for configuring the multicopter
model and flight environment parameters, where readers can select propulsion system
components to assemble different types of multicopters for subsequent simulations.
FigureA.2b is the model parameter calculation and database management interface,
which is mainly used to calculate the model parameters of the assembled multicopter
and store the results into the database for subsequent use with convenient database
management functions. FigureA.2c is the advanced function area, including swarm
simulation, UE4 scene selection, and other functions, which will be described in
detail later. FigureA.2d is mainly used to connect the Pixhawk autopilot and control
the start and stop of the simulation. FigureA.2e is used to display the real-time
message received from the Pixhawk autopilot as well as the position and attitude
information of the simulated vehicle model.

.. figure:: /images/Quan-app1-FigA.2.jpg
    :align: center

    Fig. A.2 CopterSim interface after registration


Custom Multicopter Configuration
-----------------------------------

In the first line of the model configuration interface shown in Fig.A.2a, the 
configurable parameters include basic information such as the total weight, diagonal size,
and flight altitude. In the second to the fifth rows of Fig.A.2a, readers can select the
propulsion system components or parameters for the multicopter components, such
as motors, propellers, ESCs, and batteries. CopterSim offers two options for selecting
propulsion components. As shown in Fig.A.3, the first is to assemble a multicopter
directly from the propulsion system branded model database which covers many
common products on the market.


.. figure:: /images/Quan-app1-FigA.3.jpg
    :align: center

    Fig. A.3 Custom model parameter input interface

Since the propulsion system product database is difficult to cover all of the products 
in the world, CopterSim also provides a function to customize the component
parameters which enables a more flexible way to configure a multicopter model. As
shown in Fig.A.3a, click on the “Custom Design” option at the end of the first line
to enter the component custom parameter interface shown in Fig.A.3b. In this interface, 
readers can customize the detailed parameters of motors (KV value, no-load
voltage, internal resistance), ESCs, batteries, and propellers. In theory, by using the
“Custom Design” function, readers can simulate any propulsion system components,
even products that do not exist on the market.

After a multicopter model is configured, clicking on the “Calculate” button in
Fig.A.2b will automatically analyze the feasibility of the inputted multicopter 
configuration. Unpractical multicopter configurations may cause simulation failures, such
as insufficient thrust to take off, ESC and motor overheat due to excessive battery
voltage, or the propeller size is too large for the fuselage. As shown in Fig.A.4, after
checking the inputted multicopter configuration, CopterSim will prompt a warning
dialog if the configuration is unpractical, and the reader needs to re-select a 
practicable multicopter configuration.

.. figure:: /images/Quan-app1-FigA.4.jpg
    :align: center

    Fig. A.4 Model configuration feasibility detection warning dialog

For beginners or readers who are not familiar with multicopter design, it is a
difficult task to configure a multicopter that can work. So CopterSim also provides
a convenient function to directly select vehicle configurations through a prepared
model database. As shown in Fig.A.5, in the drop-down list of the “Model Database”
item, the reader can select a usable multicopter configuration (or modify parameters
based on it) to quickly obtain the multicopter model for simulations.

After configuring a multicopter through the three methods mentioned above, clicking 
the “Add to Database” button shown in Fig.A.5 will store the new model into
the model database for use in the future. Readers can also delete the current model
from the database by clicking the “Delete from Database” button shown in Fig.A.5.

.. figure:: /images/Quan-app1-FigA.5.jpg
    :align: center

    Fig. A.5 Multicopter model selection from model database


Set Initial States
---------------------

As shown in Fig.A.2c, CopterSim provides an interface to modify the multicopter
initial position and altitude. As shown in Fig.A.6, readers can enter the “x” and “y”
coordinates (unit: m) of the multicopter and the value of the yaw angle (unit: degree),
where the x-direction and y-direction point to the front and right of the multicopter,
and the yaw angle is positive when rotating to right side.


.. figure:: /images/Quan-app1-FigA.6.jpg
    :align: center

    Fig. A.6 Setting initial simulation position
