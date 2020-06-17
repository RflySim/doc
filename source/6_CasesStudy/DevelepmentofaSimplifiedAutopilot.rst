======================================
Develepment of a Simplified Autopilot
======================================


Control Framwork
--------------------------------

Using Simulink's graphical user interface, the hierarchical design of the flight control can be easily carried out, so that the whole system structure is clear and easy to maintain. In general, the overall structure of the flight control system can be divided into two levels: high-level applications include state machine and autonomous flight, and low-level applications include position control, attitude control, and state estimator. 

    .. figure:: /images/Case1.png
        :align: center

At the same time, to focus on the design we are interested in, we do not need to design each part by ourselves from scratch. On the other hand, many functions of Pixhawk/PX4 autopilot have been successfully tested and applied. We can fully use the existing functions of this open-source system. For example, we only design the controller and state machine based on the state estimator from the current estimator in the Pixhawk/PX4 autopilot. Beginners and developers can open the module and replace it with their algorithms or add a new module such as filter for their purpose. It is easy to interact in the GUI interface. 

    .. figure:: /images/Case2.png
        :align: center


System Analysis
--------------------------------

When deploying algorithms in an embedded system, real-time performance of the algorithm is a very noteworthy issue. For control algorithms, the real-time performance is particularly important because it directly affects the bandwidth and robustness of the control system. We use the time-triggered method to ensure the algorithm runs at a stable frequency, and it can be easily implemented in Simulink with Stateflow schedulers. The underlying control logic of flight control generally adopts hierarchical control. The data update frequency of the sensor in Pixhawk/PX4 autopilot is 250Hz, so we set the execution frequency of the attitude controller to 250Hz. The control frequency of the position control is generally lower than the attitude control, and the bandwidth of the attitude control should be 4 to 10 times of position control, so the execution frequency of the position control is set to 50Hz. The high-level controller does not need a high execution frequency, so the execution frequency of the state machine is set to 5 Hz, and the autonomous flight is set to 50 Hz. The estimator in Pixhawk/PX4 autopilot is directly used for state observation. This further demonstrates the superiority of our platform. Instead of building our flight control system from scratch, we focus mainly on the areas we are interested in, such as the design of attitude control, or state machine.

    .. figure:: /images/Case3.png
        :align: center

Through the data recording function, the execution period of each module is obtained. It can be seen that the execution cycle of each module of the system is controlled very accurately. In addition, considering the hardware resource limitation of Pixhawk, the controller or state estimator we design should not be too complicated. Some online optimization methods such as MPC cannot run in real-time with limited computing resources. The memory usage of main tasks running in Pixhawk/PX4 autopilot is shown as follow. It can be seen that the memory usage of the attitude control and position control we design is half of that the autopilot's. The CPU usage of our attitude control and position control is slightly higher than that in Pixhawk/PX4 autopilot, but the autopilot’s CPU resource remains idle for 30.95\% of the time.

    .. figure:: /images/Case4.png
        :align: center


Debug Functions
--------------------------------

To improve the development efficiency of the flight controller further, we make full use of the functions of the Pixhawk/PX4 autopilot and add the following functions to the Simulink model we built.

Online parameter tuning. Beginners and developers can modify the parameters in the Simulink model online through a ground control station, namely QGroundControl (QGC). There is no need to recompile and upload the program after each parameter modification, and it improves the program debugging efficiency.

    .. figure:: /images/Case5.gif
        :align: center

Data recording. In order to facilitate experimental analysis, any data in the Simulink model can be recorded to the SD card. The number and frequency of the recorded data can be flexibly adjusted.

Real-time data inspecting. If beginners and developers need to observe the state of the aircraft or the intermediate variables of the model in real-time during the flight, it is also very convenient to add a real-time data observation module to the Simulink model, and the data can be observed in QGC. 

    .. figure:: /images/Case6.gif
        :align: center


Attitude Control Based on ADRC Law
----------------------------------------

ADRC law is a more and more popular method in practice, with the structure of ADRC shown as follow. Obviously, it is more complex than PID controllers often used in autopilots. It will be used for testing.

    .. figure:: /images/Case7.png
        :align: center

The controller is designed in Simulink, and the SIL simulation is performed,. We can easily observe the interested states in Simulink and adjust the model to make it satisfied. After that, in the HIL simulation, only a simple modification of the model’s output is made for C/C++ code generation, but the controller will keep the same as the SIL simulation. The generated C/C++ code will be uploaded to Pixhawk automatically. Then, HIL simulation can be performed. In this process, we can manually control the multicopter and observe the aircraft’s response. Controller parameters can be adjusted according to the HIL simulation performance. Finally, the actual flight test is performed. We add 0.2kg weight to a 1.4kg multicopter as an external disturbance. Under the influence of external disturbance, the multicopter tilts slightly and then begins to adjust its attitude. After the adjustment, the multicopter returns to the horizontal state and rejects disturbance by itself. It should be noted that, based on the proposed platform, the designer only needs to design and improve the controller in Simulink. Basically, they are almost the same in SIL simulation, HIL simulation and real flight. The video can be found at https://flyeval.com/course/.

    .. figure:: /images/Case8.png
        :align: center

