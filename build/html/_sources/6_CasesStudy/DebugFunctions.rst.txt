=============================
Debug Functions
=============================

To improve the development efficiency of the flight controller further, we make full use of the functions of the Pixhawk/PX4 autopilot and add the following functions to the Simulink model we built.

Online parameter tuning. Beginners and developers can modify the parameters in the Simulink model online through a ground control station, namely QGroundControl (QGC). There is no need to recompile and upload the program after each parameter modification, and it improves the program debugging efficiency.

    .. figure:: /images/Case5.gif
        :align: center

Data recording. In order to facilitate experimental analysis, any data in the Simulink model can be recorded to the SD card. The number and frequency of the recorded data can be flexibly adjusted.

Real-time data inspecting. If beginners and developers need to observe the state of the aircraft or the intermediate variables of the model in real-time during the flight, it is also very convenient to add a real-time data observation module to the Simulink model, and the data can be observed in QGC. 

    .. figure:: /images/Case6.gif
        :align: center

