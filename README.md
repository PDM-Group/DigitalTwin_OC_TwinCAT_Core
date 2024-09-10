# Open Commissioning: TwinCAT Core Library

The TwinCAT Core Library is used in the TwinCAT PLC project and provides the behaviour models for industrial devices as function blocks.

## 1. Project setup
+ Install and add the `OC_Core` library in the PLC project with the standard library manager
+ Install the following dependencies:
  * TcUnit
  * Tc2_Utilities
  * Tc2_Math
  * Tc3_Module
+ Declare FB_System in your main program
> [!WARNING]  
> There should always be an instance of FB_System in the PLC project, otherwise the project can't be started. 
> Take a look at the logs in the console

## 2. Overview
In Unity project each device has a link class, which defines the interface for communication with TwinCAT. 
At startup, Unity Client tries to find a TwinCAT function block for each device. 
The search is done by name and type. The mapping is done when all the interface variables have found the opposite side in twincat, otherwise connection for this module becomes invalid.

![Twincat_Overview](./images/TwinCAT_Overview_dark.png#gh-dark-mode-only)
![Twincat_Overview](./images/TwinCAT_Overview_light.png#gh-light-mode-only)

## 2. Components
### 2.1 System



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

#### 2.2.1 Basic Devices
The basic Function Blocks for the most frequently used devices are listed under Basic folder in Library.
* `FB_Button`
* `FB_Cylinder`
* `FB_SensorBinary`
* `...`

#### 2.2.2 Drives
The Drive Folder collects the function blocks for various drives, such as simulation blocks for `DS402`, `SoE`, etc drives. 

#### 2.2.3 Others
The library is planned to be further developed with several functional modules in the future.





