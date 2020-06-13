=============================
Control Framwork
=============================

Using Simulink's graphical user interface, the hierarchical design of the flight control can be easily carried out, so that the whole system structure is clear and easy to maintain. In general, the overall structure of the flight control system can be divided into two levels: high-level applications include state machine and autonomous flight, and low-level applications include position control, attitude control, and state estimator. 

    .. figure:: /images/Case1.png
        :align: center

At the same time, to focus on the design we are interested in, we do not need to design each part by ourselves from scratch. On the other hand, many functions of Pixhawk/PX4 autopilot have been successfully tested and applied. We can fully use the existing functions of this open-source system. For example, we only design the controller and state machine based on the state estimator from the current estimator in the Pixhawk/PX4 autopilot. Beginners and developers can open the module and replace it with their algorithms or add a new module such as filter for their purpose. It is easy to interact in the GUI interface. 

    .. figure:: /images/Case2.png
        :align: center
