![image](images/microchip.jpg) 

# MATLAB MCLV-2 dsPIC33CK256MP508 REGENERATIVE BRAKING 

## 1. INTRODUCTION
<p style='text-align: justify;'>
This document describes the setup requirements for running the Regenerative Braking algorithm, using MATLAB Simulink, MCLV-2 Development Board and dsPIC33CK256MP508 External Op-Amp Motor Control Plug-In Module (PIM).</p>

## 2.	SUGGESTED DEMONSTRATION REQUIREMENTS
### 2.1 MATLAB Model Required for the Demonstration
-  MATLAB model can be cloned or downloaded as zip file from the Github repository ([link](https://github.com/microchip-pic-avr-solutions/matlab-mclv2-dspic33ck256mp508-regenerativebraking)).

### 2.2	Software Tools Used for Testing the MATLAB/Simulink Model
1.	MPLAB X IDE and IPE (v6.0)
2.	XC16 compiler (v2.00)
3.	MATLAB R2022a
4.	Required MATLAB add-on packages
    -	Simulink
    -	Simulink Coder
    -	Stateflow
    -	MATLAB Coder
    -	Embedded Coder (v7.8)
    -	MPLAB Device blocks for Simulink (v3.50.27)
    - Motor Control Blockset (v1.4)

> **_NOTE:_**
>The software used for testing the model during release is listed above. It is recommended to use the version listed above, or later versions, for building the model.

### 2.3	Hardware Tools Required for the Demonstration

| Hardware Tool|Part Number|Quantity|
| :-------------:| :-----------:|:--:|
|dsPICDEM™ MCLV-2 Development Board|[DM330021-2](https://www.microchip.com/en-us/development-tool/DM330021-2) |2 |
|dsPIC33CK256MP508 External Op-Amp Motor Control Plug-In Module|[MA330041-1](https://www.microchip.com/en-us/development-tool/MA330041-1)|2|
|Benchtop power supply (compatible 24V, 5A)|-|1|
|24V 3-Phase Brushless DC Motor with Encoder|[AC300022](https://www.microchip.com/en-us/development-tool/AC300022)|2|
|USB to RS-232 cable|-|2|

> **_NOTE:_**
><p style='text-align: justify;'>The two motors shafts are coupled together. The fixture of both motors coupled together is not sold by Microchip Technology. The fixture was created only for this demonstration purpose. Any standard motor shaft coupler can be used with 8mm diameter on both the sides.</p>

  
## 3. HARDWARE SETUP
<p style='text-align: justify;'>This section describes the hardware setup needed for the demonstration. In this demonstration two MCV-2 boards are used to control the motor and the generator. The MCLV-2 board connected to the motor is referred as ‘the motor side MCLV-2 board’ and the MCLV-2 board connected to the generator is referred as ‘the generator side MCLV-2 board’</p>

1. <p style='text-align: justify;'> Disconnect power to the MCLV-2 Boards and set up the following jumpers:</p>

    <p align="left" >
    <img  src="images/pic1.png"></p>

2. <p style='text-align: justify;'> On both the boards, insert the ‘External Op Amp Configuration Matrix board’ into matrix board header J14. Ensure the matrix board is correctly oriented before proceeding.</p>

    <p align="left" >
    <img  src="images/pic2.png"></p>

3. <p style='text-align: justify;'> Insert the dsPIC33CK256MP508 External Op-Amp Motor Control PIM into the PIM Socket U9 provided on the MCLV-2 Boards. Make sure the PIM is correctly placed and oriented before proceeding.</p>

    <p align="left" >
    <img  src="images/pic3.jpg"></p>

4. <p style='text-align: justify;'>	Connect the three phase wires from the motor to M1, M2, and M3 terminals of connector J7, on ‘the motor side MCLV-2 Board’ in the sequence as shown below. </p>

    <p align="left" >
    <img  src="images/pic4.jpg"></p>

5. <p style='text-align: justify;'>	Connect the three phase wires from the generator to M1, M2, and M3 terminals of connector J7, on the ‘generator side MCLV-2 Board’. Please note that for sequence of 3 phase wires and the encoder wires sequence must be as shown below.</p>

    <p align="left" >
    <img  src="images/pic5.png"></p>

6. <p style='text-align: justify;'>	Set 24V on the benchtop power supply and connect it to the connectors BP1 and BP2 provided on both the MCLV-2 Boards (The single power supply is used for both the MCLV-2 boards). Couple the motors shafts using a coupler and connected to MCLV-2 boards. Make sure the setup is as shown below.</p>

    <p align="left" >
    <img  src="images/pic6.png"></p>

7. <p style='text-align: justify;'>	The Microchip MPLAB PICkit 4 In-Circuit Debugger needs to connected to the Connector J12 of the MCLV-2 Board, as shown below. Also connect to the Host PC used for programming the device.. Ensure the arrows indicated on the board and  PICkit 4 orient as shown in the picture. </p>

    <p align="left" >
    <img  src="images/pic7.png"></p>

> **_NOTE:_**
>It is recommended to use a right-angled pin header to use J12 for programming. A straight header mounted with PICkit 4 may result in mechanical stresses on the programmer con-nector or the development board in use.

  <p style='text-align: justify;'>	Alternatively, the programmer/debugger can be connected to J11 using a RJ-11 to ICSP adapter (AC164110).</p>

  <p align="left" >
  <img  src="images/pic7_1.png"></p>

## 4.	BASIC DEMONSTRATION
<p style='text-align: justify;'> Follow the below instructions step-by-step, to set up and run the motor control demo application:</p>

1. Launch MATLAB (refer the section [“2.2 Sofware Tools Used for Testing the MATLAB/Simulink Model"](#22-software-tools-used-for-testing-the-matlabsimulink-model)).</p> 
2. Open the folder dowmloaded from the repository, in which MATLAB files are saved (refer the section ["2.1 MATLAB Model Required for the Demonstration"](#21-matlab-model-required-for-the-demonstration)).

    <p align="left" >
    <img  src="images/dem1.png"></p>

    In this folder there will be five files used for the demonstration, 
    |File Name|Description|
    | :-------------:| :-----------:|
    |dsPIC33CK256MP508_MCLV2_Generator_data.m|Data file for generator side Simulink model|
    |dsPIC33CK256MP508_MCLV2_QEI_Generator.slx|Simulink model for ‘the generator side MCLV-2 board’ using optical encoder|
    |dsPIC33CK256MP508_MCLV2_SMO_data.m|Data file for motor side Simulink model|
    |dsPIC33CK256MP508_MCLV2_SMO_Motor.slx|Simulink model for ‘the motor side MCLV-2 board’ using Sliding motor observer|
    |mcb_host_common.slx|Simulink model to monitor real time parameters from the hardware|

3.	Connect the PICkit 4 In-Circuit Debugger to the Connector J12 of ‘motor side MCLV-2 Board’, as mentioned in the step 7 of the ["3.3 Hardware Setup"](#3-hardware-setup) section and turn on the power supply.

4.	<p style='text-align: justify;'> Double click and open the <b>dsPIC33CK256MP508_MCLV2_SMO_data.m</b> file. This file contains the configuration parameter for the motor and board. By default, the file is configured to run Hurst 300 motor and MCLV-2 board. Run the file by clicking the <b>“Run”</b> icon and wait till all variables get loaded on the <b>‘Workspace’</b> tab.</p>

    <p align="left">
      <img  src="images/dem3.png"></p>
    </p>

5.	<p style='text-align: justify;'>Double click on <b>dsPIC33CK256MP508_MCLV2_SMO_Motor.slx</b> Simulink model.</p>

    <p align="left">
      <img  src="images/dem4.png"></p>
    </p>

6.	<p style='text-align: justify;'>This opens the Simulink model, as shown below.  

    <p align="left">
      <img  src="images/dem5.png"></p>
    </p>

7.	<p style='text-align: justify;'>From this Simulink model an MPLAB X project is generated, and it can be used to run the motor using MCLV-2 board. To generate the code from the Simulink model, go to the <b>“MICROCHIP”</b> tab, and enable the tabs shown in the figure below. 

    <p align="left">
      <img  src="images/pic12.png"></p>
    </p>

8.	<p style='text-align: justify;'>	To generate the code and program the dsPIC33CK256MP508 device, click on <b>‘Build Model’ or ‘Clean Build Model’</b> option under the <b>“Microchip”</b> tab. This will generate the MPLAB X project from the Simulink model.

    <p align="left">
      <img  src="images/dem8.png"></p>
    </p>

9.	<p style='text-align: justify;'>After completing the process, the <b>‘Operation Succeeded’</b> message will be displayed on the <b>‘Diagnostics Viewer’</b>.

    <p align="left">
      <img  src="images/pic15.png"></p>
    </p>

10.	If the device is successfully programmed, <b>LED- LD10 and LD11</b> will be blinking.

11. <p style='text-align: justify;'>Now connect the PICkit 4 In-Circuit Debugger to the Connector J12 of generator side MCLV-2 Development Board. </p>

12. To program the generator side dsPIC33CK256MP508 device repeat the step 4 to 10, using the <b>dsPIC33CK256MP508_MCLV2_Generator_data.m</b> and <b>dsPIC33CK256MP508_MCLV2_QEI_Generator.slx</b>  files.

13.	To run the setup, press the push button <b>S2</b>of the motor side MCLV-2 board first and then the generator side MCLV-2 board.

    <p align="left">
      <img  src="images/pic18.png"></p> 
    </p>

14.	The motor speed can be varied using the potentiometer (labeled <b>“POT1”</b>) of the motor side MCLV-2 board. The regenerative torque can be varied using the potentiometer (labeled <b>“POT1”</b>) of the generator side MCLV-2 board.

15.	Press the push button <b>S2</b> of the motor side and generator side MCLV-2 to stop the operation.


## 5.	DATA MONITORING USING MOTOR CONTROL BLOCKSET (MCB) HOST MODEL
<p style='text-align: justify;'>The regenerative braking simulink models comes with the initialization required for data monitoring using Motor Control Blockset Host Model (MCB Host Model). The MCB Host Model is a Simulink model which facilitates data monitoring through the UART Serial Interface. 

1.	<p style='text-align: justify;'>To establish serial communication with the host PC, connect a USB to RS-232 cable between the host PC and the MCLV-2 Board (J10 connector) of both motor and generator side.
    <p align="left">
      <img  src="images/pic21.png"></p>
    </p>

2. Ensure the sensorless FOC model is programmed and running as described under section ["4. Basic Demonstration"](#4-basic-demonstration) by following steps 1 through 14.

3. <p style='text-align: justify;'>Open the MCB Host model (mcb_host_common.slx)

    <p align="left">
      <img  src="images/host3.png"></p>
    </p>

4.	<p style='text-align: justify;'>Double click on the  the <b>“Motor_Rx”</b> block. Then select the appropriate COM port which is connected to the motor side MCLV-2 board from the drop-down menu and set the baud rate as 115207. Please note that the same baud rate has been set in the motor side Simulink model (the baud rate can be viewed on the <b>“UART Configuration block”</b> in the <b>“Hardware Init”</b> subsystem).

    <p align="left">
      <img  src="images/host4.png"></p>
    </p>

5.	<p style='text-align: justify;'>Open the <b>“Motor_Rx”</b> subsystem to configure the COM port. This can be done by configuring the <b>“Host Serial Receive”</b> block of the <b>“Motor_Rx”</b> subsystem. Ensure to select the same COM port configured in step 4.
    <p align="left">
      <img  src="images/host5.png"></p>
    </p>

6. <p style='text-align: justify;'>Similarly, double click on the <b>“Generator Serial Setup”</b> block. Then select the appropriate COM port which is connected to the genrator side MCLV-2 board from the drop-down menu and set the baud rate as 115207. Please note that the same baud rate has been set in the generator side Simulink model (the baud rate can be viewed on the <b>“UART Configuration block”</b> in the <b>“Hardware Init”</b> subsystem).
    <p align="left">
      <img  src="images/host6.png"></p>
    </p>

7. <p style='text-align: justify;'>Open the <b>“Generator_Rx”</b> subsystem to configure the COM port. This can be done by configuring the <b>“Host Serial Receive”</b> block of the <b>“Generator_Rx”</b> subsystem. Ensure to se-lect the same COM port configured in step 6.

    <p align="left">
      <img  src="images/host7.png"></p>
    </p>

8. <p style='text-align: justify;'>Click the run icon of the MCB Host model to open the scope window and monitor the signals.

    <p align="left">
      <img  src="images/host8.png"></p>
    </p>

9.	<p style='text-align: justify;'>Figure below shows an example of monitored signals using the MCB Host Model. 

    <p align="left">
      <img  src="images/host9.png"></p>
    </p>


## 	REFERENCES:
For more information, refer to the following documents or links.
1.	AN1078 Application Note “[Sensorless Field Oriented Control of a PMSM](https://www.microchip.com/en-us/application-notes/an1078)”.
2.	dsPICDEM™ MCLV-2 Development Board User’s Guide  ([DS52080A](https://ww1.microchip.com/downloads/en/DeviceDoc/DS-52080a.pdf)) 
3. dsPIC33CK256MP508 Motor Control Plug-In Module (PIM) Information Sheet for External Op Amp Configuration ([DS50002757A](http://ww1.microchip.com/downloads/en/DeviceDoc/dsPIC33CK256MP508-Motor-Control-PIM-for-External-Op-Amp-Configuration-DS50002757A.pdf))
4.	[MPLAB® X IDE installation](https://microchipdeveloper.com/mplabx:installation)
5.	[MPLAB® XC16 Compiler installation](https://microchipdeveloper.com/mplabx:installation)
6.  [Motor Control Blockset](https://in.mathworks.com/help/mcb/)
7.  [MPLAB Device Blocks for Simulink :dsPIC, PIC32 and SAM mcu](https://in.mathworks.com/matlabcentral/fileexchange/71892-mplab-device-blocks-for-simulink-dspic-pic32-and-sam-mcu)