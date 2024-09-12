# Open Commissioning: TwinCAT Core Library

The TwinCAT Core Library is used in the TwinCAT PLC project and provides the behaviour models for industrial devices as function blocks.

## 1. Project setup
+ Create PLC Project
+ Install and add the `OC_Core` library
+ Install the dependencies:
  * TcUnit
  * Tc2_Utilities
  * Tc2_Math
  * Tc3_Module
+ Declare and call `FB_System` in your main program

## 2. Overview
In Unity project each device has a link class, which defines the interface for communication with TwinCAT. 
At startup, Unity Client tries to find a TwinCAT function block for each device. 
The search is done by name and type. The mapping is done when all the interface variables have found the opposite side in twincat, otherwise connection for this module becomes invalid.

![Twincat_Overview](./images/TwinCAT_Overview_dark.png#gh-dark-mode-only)
![Twincat_Overview](./images/TwinCAT_Overview_light.png#gh-light-mode-only)

## 2. Components
### 2.1 System
The main component in Open Commissioning is `FB_System`. 
This function block contains the system parameters and the global system variables such as `fDeltatime`, which can be accessed by other FBs in the project through the static `GVL_Core.fbSystem`.
`FB_System` should be defined and called up once in the project so that the GVL reference is correctly assigned. 
If `FB_System` is not defined or there are several instances, the TwinCAT PLC project is forced into config mode with corresponding messages in the console.

### 2.2 Links
The links are the basic communication blocks in open commissioning that realise the interface for data exchange.

The basic interface consists of a `Control` _(From TwinCAT to Unity)_ and `Status` _(From Unity to TwinCAT)_ byte. 
The basic link is used for additional data exchange and extended with corresponding data types. The current library contains the following links:
* `FB_LinkDevice`
* `FB_LinkDataByte`
* `FB_LinkDataWord`
* `FB_LinkDataDWord`
* `FB_LinkDataLWord`
* `FB_LinkDataReal`

### 2.3 Devices
Device in Open Commissioning is a function block that represents the behaviour of the device at PLC level. 
If device is inherited from an FB_Link, the corresponding interface is also prepared for Unity. 
Devices also have the interface to the PLC side. 
This can be as single variables or complex structures, such as control and status words in drive systems.

An example of the abstracted `FB_Drive` is shown in the following images.
![Device_Example1](./images/Device_Example1_dark.png#gh-dark-mode-only)
![Device_Example1](./images/Device_Example1_light.png#gh-light-mode-only)

#### 2.2.1 Basic
The basic Function Blocks for the most frequently used devices are listed under Basic folder in Library.
* `FB_Button`
* `FB_Cylinder`
* `FB_SensorBinary`
* `...`

#### 2.2.2 Drives
The Drive Folder collects the function blocks for various drives, such as simulation blocks for `DS402`, `SoE`, etc drives. 

#### 2.2.3 Others
The library is planned to be further developed with several functional modules in the future.


## 4. Contributing
Pull requests, bug reports, and all other forms of contribution are welcomed and highly encouraged!
Please review our Contributing Guidelines. 

### 4.1 Programming Conventions
[Beckhoff Programming Conventions](https://infosys.beckhoff.com/english.php?content=../content/1033/tc3_plc_intro/12049233675.html&id=6398798947359024199) are used in this project.



