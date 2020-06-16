==============================
Software Package Installation
==============================

The installation process of the Simulation Software Package is highly automated
and readers can run a one-click installation script to achieve rapid and automatic
deployment.

Installation Steps
--------------------

The installation steps are summarized below.

(1) Download the installation image file “RFLYExpPspSoftwarePack.iso” of the
Simulation Software Package from :doc:`Download and Support<../7_DownloadAndSupport/DownloadAndSupport>`, 
and then unzip it or mount it to a virtual drive folder.

(2) Open MATLAB and click the “Browse for Folder” button (see Fig. 2.3). On the
folder selection window, select the folder “RFLYExpPspSoftwarePack” obtained
in the previous step.

(3) As shown in Fig. 2.3, tap the command “PX4InstallScript” in the “Command
Window” of MATLAB and press the “Enter” key on the keyboard to run the
one-key installation script. Note that another convenient way to run the one-key
script is to select the “PX4InstallScript.p” file (see Fig. 2.3) with the mouse right
key, and click the “Run” button on the pop-up menu.

    .. figure:: /images/Quan-ch2-Fig2.3.jpg
        :align: center

        Fig. 2.3 Installing multicopter simulation software package with one-click installation script

(4) In the pop-up configuration window shown in Fig. 2.4, select the required 
configuration according to the actual hardware and software requirements (the default
configuration is recommended for beginners, where the compiling command is
px4fmu-v3_default, the PX4 firmware version is 1.7.3, and the installation 
directory is the C disk, which may occupy around 6G storage), and click the “OK”
button in Fig. 2.4.

    .. figure:: /images/Quan-ch2-Fig2.4.jpg
        :align: center

        Fig. 2.4 Options of PX4InstallScript

(5) Wait patiently for the package to be successfully installed and deployed, which
may take around 30 min.

**Noteworthy** :

(1) Antivirus software may prevent this script from generating desktop shortcuts.
If the script prompts that the shortcut generation has failed, please close the
antivirus software (Windows 10 should also turn off the “Real-time protection”
option in the Settings page) and manually click the “GenerateShortcutCMD.bat”
script in the installation directory (the default directory is C:\PX4PSP) to 
automatically generate all the software shortcuts.

(2) If readers want to change the firmware configurations or restore the 
compiling environment, just run the “PX4InstallScript” command again and select the
required options.

(3) Readers can check the document “readme.txt” in the folder “RFLYExpPspSoftwarePack” 
for more detailed notes.


Advanced Settings
--------------------

For advanced independent developers, Fig. 2.4 provides options to select the installation directory, Pixhawk hardware version, PX4 firmware version, compiling command, compiling environment, etc. The options in Fig. 2.4 are explained in detail
below.

(1) **Software package installation directory** . All dependent files on the software
package are installed in this directory, which requires around 6G storage. The
default installation directory is “C: \PX4PSP”. If the C disk space is not suffi-
cient, readers should choose a directory in other disks; the directory name must
be correct and only in English to prevent compilation failures.

(2) **PX4 firmware compiling command** . The default compiling command for PX4
is “px4fmu-v3_default”. By selecting this compiling command, the compiling
toolchain is automatically called to compile the PX4 source code to a firmware
file “px4fmu-v3_default.px4” after the PSP generates the controller code. Then,
the file “.px4” is uploaded to the supported hardware to realize the deployment
of the control algorithms. Different Pixhawk hardware products must select
different PX4 firmware compiling commands. Figure 2.5 shows some Pixhawk
hardware products, where “px4fmu-v3_default” can be used for three popular
products: Pixhawk 1 (2MB flash version), mRo `Pixhawk <https://docs.px4.io/master/en/flight_controller/mro_pixhawk.html.>`_ 
and Cube (`Pixhawk 2 <https://docs.px4.io/master/en/flight_controller/pixhawk-2.html>`_ ). 
The command “px4fmu-v2_default” corresponds to the most famous `Pixhawk 1 <https://docs.px4.io/master/en/flight_controller/pixhawk.html>`_ . 
PX4 also supports other hardware (for example, `Intel Aero <https://software.intel.com/en-us/aero/drone-kit>`_ , 
`Crazy-flie <https://www.bitcraze.io/crazyflie-2/>`_ , and so on). 
The corresponding compiling `commands <http://dev.px4.io/master/en/setup/building_px4.html>`_ 
are listed below. 

* Pixhawk 1: px4fmu-v2_default.px4
* Pixhawk 1 (2MB flash version): px4fmu-v3_default.px4
* Pixhawk 4: px4fmu-v5_default
* Pixracer: px4fmu-v4_default
* Pixhawk 3 Pro: px4fmu-v4pro_default
* Pixhawk Mini: px4fmu-v3_default
* Pixhawk 2: px4fmu-v3_default
* mRo Pixhawk: px4fmu-v3_default
* HKPilot32: px4fmu-v2_default
* Pixfalcon: px4fmu-v2_default
* Dropix: px4fmu-v2_default
* MindPX/MindRacer: mindpx-v2_default
* mRo X-2.1: auav-x21_default
* Crazyflie 2.0: crazyflie_default
* Intel Aero Ready to Fly Drone: aerofc-v1_default.

    .. figure:: /images/Quan-ch2-Fig2.5.jpg
        :align: center

        Fig. 2.5 Pixhawk hardware series products with compiling commands

(3) **PX4 firmware version** . The version of the PX4 source code is updated 
constantly, and the latest firmware version was 1.10 when this book was written. As
the firmware version is upgraded, new features may be introduced, and more
new products will be supported, but the compatibility with some old 
autopilot hardware will be affected. Because the Pixhawk 1 (2MB flash version, or
mRo Pixhawk) hardware selected in this book is an old Pixhawk product with
LED for better experimental observation effect, the older PX4 firmware 
version 1.7.3 was selected with the compiling command “px4fmu-v3_default” to
achieve better-using effect.

(4) **PX4 firmware compiling toolchain** . Because the compilation of PX4 source
code depends on the Linux compiling environment, the software package provides three sets of compiling toolchains to realize the simulation of the Linux
compiling environment under the Windows environment.

    1) `Win10WSL <https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux>`_ based on the Windows Subsystem compiler environment for Linux (WSL);
    2) the Msys2Toolchain based on `Msys2 <https://baike.baidu.com/item/MSYS2>`_ toolchain;
    3) the CygwinToolchain based on the `Cygwin <https://www.cygwin.com/>`_ toolchain.

    .. note:: the CygwinToolchain only supports PX4 firmware with version
        1.8 or above; the Msys2Toolchain only supports PX4 firmware with version
        1.8 or below. Both the CygwinToolchain and the Msys2Toolchain support
        Windows 7 and above, which are easy to deploy, but the compiling speed
        is slow. For Windows10 1809 and above, readers can follow the tutorial in
        “0.UbuntuWSL\Win10UbuntuInstallationStep.docx” to install an Ubuntu subsystem in
        Windows and then choose theWin10WSL toolchain shown in Fig. 2.4.
        The Win10WSL toolchain can greatly accelerate the compiling speed and support 
        all versions of PX4 firmware.

(5) **Whether to reinstall the PSP Toolbox (yes or no)** . If this option is set to
“yes”, the PSP Toolbox is installed on MATLAB/Simulink. If the PSP toolbox
has already been installed, a new installation of the PSP Toolbox is performed.
If this option is set to “no”, the script does not do anything on the existing PSP
toolbox (it will not uninstall the PSP toolbox or carry out other actions).

(6) **Whether to reinstall the dependent software packages** . If this option is set
to “yes”, software tools (such as FlightGear, QGC, CopterSim, and 3DDisplay)
are deployed to the selected installation directory and shortcuts for them are
generated on the desktop. The related drivers for Pixhawk hardware are also
installed. If the software tools have already been installed, selecting “yes” will
remove the old installation files and reinstall them. If this option is set to “no”,
then no change will be made.

(7) **Whether to reinstall the selected compiling toolchain** . If this option is set
to “yes”, the selected compiling toolchain (Win10WSL, CygwinToolchain, or
Msys2Toolchain) will be deployed to the selected installation directory. If the
toolchain already installed, the script will remove the old toolchain files and
reinstall it. In contrast, if this option is set to “no”, then no change will be made.

(8) **Whether to reinstall the selected PX4 firmware source code** . If this option
is set to “yes”, the selected PX4 firmware source code will be deployed to
the selected installation directory. If the firmware files already exist, the old
firmware folder will be deleted, and a new copy of the source code will be
deployed. If this option is set to “no”, then no change will be made.

(9) **Whether to pre-compile the selected firmware** . If this option is set to “yes”,
the PX4 source code will be pre-compiled. This can greatly save the compiling
time of the subsequent code generation process; whether the compiling environment 
is installed properly can also be checked. If this option is set to “no”,
then no change will be made.

(10) **Whether to block the actuator outputs of the PX4 original controller** . If
this option is set to “yes”, the control signals of the PX4 original controller will
be blocked to prevent them from conflicting with the generated controller in
Simulink. This option must be set to “yes” for the simulations and experiments
in this book. If this option is set to “no”, the PX4 outputs will not be blocked,
and this mode can be used to test the PX4 original controller.

    .. note::

        For the firmware versions 1.9 and above, the PX4 starts to use new compiling 
        commands with the form “px4_fmu-v3_default.px4” instead of “px4fmu-v3_default.px4”.
        Because the simulation software package of this book will be continuously updated
        for the latest PX4 firmware when using the latest version of the firmware (1.9 and
        above), readers need to modify the compiling command in Fig. 2.4 to the correct
        format.


Installation Completion
-------------------------

When the above one-key installation scripted is successfully executed, readers can
check the installed content with the following procedure.

(1) As shown in Fig. 2.6, the shortcuts for the core software tools will be generated
on the desktop.

.. figure:: /images/Quan-ch2-Fig2.6.jpg
    :align: center

    Fig. 2.6 Desktop shortcuts of simulation software package

(2) As shown in Fig. 2.7, the folders of all software tools are stored in the selected
installation directory (the default is “C:\PX4PSP”). Note that all the software
tools are completely portable and independent of the original software (e.g.,
official versions of QGC and FlightGear) on Windows. In Fig. 2.7, the folder
“Firmware” stores the PX4 source code. The folder “examples” stores Simulink
source code examples of the PSP toolbox; the folder “drivers” stores Pixhawk
drivers. The folder “Python27” stores a Python environment for the automatic
firmware uploading of the PSP toolbox. The names of other folders are the same
as the software names, whose detailed introduction can be found in Sect. 2.1.2.

.. figure:: /images/Quan-ch2-Fig2.7.jpg
    :align: center

    Fig. 2.7 All files in installation directory of simulation software package

(3) As shown in Fig. 2.8, the installed PSP toolbox can be found on the “Add-Ons” -
“Manage Add-Ons” page of MATLAB. On this page, some management operations can 
be performed for the PSP toolbox that includes disabling, uninstalling,
and viewing the installation directory. Note that the PSP toolbox can be installed
once for all the MATLAB applications on a computer whose versions are higher
than or equal to MATLAB R2017b.

.. figure:: /images/Quan-ch2-Fig2.8.jpg
    :align: center

    Fig. 2.8 PSP Toolbox management page in MATLAB

(4) As shown in Fig. 2.9, readers can open any Simulink file and click the “Simulink
Library Brower” button to open the Simulink library browser, and then find the
“Pixhawk Target Blocks” library generated by the PSP toolbox.

.. figure:: /images/Quan-ch2-Fig2.9.jpg
    :align: center

    Fig. 2.9 PSP toolbox in Simulink library browser

If readers want to uninstall the simulation software package, they can carry out
the following steps:

(1) Delete all the desktop shortcuts presented in Fig. 2.6;
(2) Delete all files and folders in the installation directory presented in Fig. 2.7;
(3) In the “Management Additional Functions” page of MATLAB presented in Fig. 2.8, click the “Uninstall” button to uninstall the PSP toolbox.


Brief Introduction to Software
-------------------------------

(1) Double-click the desktop shortcuts shown in Fig. 2.6, which include 
“FlightGearF450”, “CopterSim”, “QGroundControl” and “3DDisplay”. Then, check the
software User Interface (UI) one by one with Fig. 2.10 to confirm that each
software can operate correctly.

.. figure:: /images/Quan-ch2-Fig2.10.jpg
    :align: center

    Fig. 2.10 Basic software UIs for simulation tools

(2) Double-click the desktop shortcut “Eclipse” in Fig. 2.6 to open the Eclipse 
software. As shown in Fig. 2.11, click “File” – “Import...” – “C/C++”—“Existing
Code as Makefile Project” from the menu bar of the Eclipse, and then click
“Next”. In the “Existing Code Location” section of the pop-up window, click
the “Browse” button to locate the “Firmware” folder in the installation directory
(default is “C:\PX4PSP”), then choose “Cross GCC” and click the “Finish” button.

.. figure:: /images/Quan-ch2-Fig2.11.jpg
    :align: center

    Fig. 2.11 Importing PX4 Firmware source code into Eclipse

After completing the above steps, as shown in Fig. 2.12, the source code and
directory structure of the “Firmware” can be found in the “Project Explorer” 
window, where readers can read the PX4 source code and try to modify it. Readers
can also view the PX4 developer documentation `website <http://dev.px4.io/master/en/index.html>`_ 
to clearly understand
the architecture and implementation principles of the PX4 algorithms and deepen
the understanding of an actual flight control system. Note that: a “Welcome” tab
will cover the content shown in Fig. 2.12 when readers first open Eclipse, it must
be closed manually.

.. figure:: /images/Quan-ch2-Fig2.12.jpg
    :align: center

    Fig. 2.12 Eclipse code reading interface

(3) Double-click one of the three shortcuts “Win10WSL”, “Msys2Toolchain” or
“CygwinToolchain” on the desktop to pop up the command window interface
shown in Fig. 2.13 (the original UI has a pure black background, and the image
color has been reversed for reading). Because the compiling toolchains are 
essentially Linux emulation software, the basic Linux commands (such as “ls”, “pwd”,
and “gcc—version”) can be tapped on the command line. For readers who are
unfamiliar with Linux operations, this compiling toolchain can also be used as a
Linux learning and practice tool. The most important function of this toolchain
is to compile the source code of PX4 and generate the “.px4” firmware file.
As shown in Fig. 2.13, “make clean” can be tapped on the command line to
clear the old compiling files, and the “make px4fmu-v3_default” command is
used to compile the source code to the firmware file “C:\PX4PSP\Firmware\
build\px4fmu-v3_default\px4fmu-v3_default.px4” for Pixhawk 1 (2MB flash
version). Because the PSP toolbox will automatically call this compiling 
command after the code is generated, readers do not need to know how to use it.

.. figure:: /images/Quan-ch2-Fig2.13.jpg
    :align: center

    Fig. 2.13 Commands tapped in compiling toolchains
