==============================
Vision-based Control Interface
==============================

As shown in Fig.A.24, the provided UE4 3D display software also supports a view
switching function to easily acquire image data from multiple viewing angles. The
image data can be acquired and processed in real-time through Simulink, Python,
C/C++, and other code platforms through shared memory inter-process communication. 
The obtained vision data can be returned to CopterSim or Simulink control
through the UDP network to form a HIL simulation loop with vision feedback.

.. figure:: /images/Quan-app1-FigA.24.jpg
    :align: center

    Fig. A.24 Different views of a car
