 # **CHANGELOG ET V3.1.x.x**

## Unreleased
- no unreleased features yet


## [V3.1.2.2] - development 2025-11-28

### Changed
- Motion/TF5100-NCI/NciChannel
	- Removed Eventlogger FB
	
- StringHelper/ExtendedString
	FBs ExtString and ExtWString, renamed method LEN to LENGTH to avoid compiler msg C0508
	
- Eventlogger/ReadEvents
	EVENTLOG_READ_DATA renamed var Class to eClass of event calls to avoid compiler msg C0543

- Logging/Logbook_wEventClass
	Renamed var Class to eClass of event calls to avoid compiler msg C0543
	
### Added
- Motion/TF5100-NCI/NciChannel_wEvents
	- Added NciChannel_wEvents including legacy Eventlogger FBs 
	
- IO/Analog/FB AnalogIn
	- Added new Option/method "optEnableScaleExtRangeModeNeg7629" to enable a min scale value of -7629 for 4-20mA scaling in ExtendedRange mode of new 16bit analog terminals 
	
- IO/Motors/ FB IOMotor2Dir
	- Added error check of ProtSwitchOK to method switchOff (similar to IOMotor FB)
	
- StringHelper
	- Added new function cutStrToSeperator2 with pointer input to work in string variables with variable lenght 
	
### Fixed
- Motion/TF5100-NCI/01_Main/NciAdmin
	- Fixed to show error in case FB un-group goes into error state (e.g. due to slave axis coupled to NCI group axis)
	
- Connectivity/TF6310-TcpServer/UdpBasic/FB UDPSendRecCtrl 
	- Writing output variables RecRemoteHost and RecRemotePort in receive method

## [V3.1.2.1] - development 2025-08-05

### Changed 
- Statemodel/control
	- Change to ABORTED when local EStopDel changed to FALSE even if Master EStop delay already elapsed 
	- Even if RemoteCtrl of Slave is disabled, Master will still check and react to slave machine error 
	(Set option.4/OPTION_ENABLE_MASCHINE_ERROR_TO_MASTER to false to disconnect Slave from Master completely)

### Added
- Motion/TF50xx-NC/00_Base/AxPara
	- New output variable DriveType
	- Properties with data type ENUM for encoder, drive and axis type
		
### Fixed
- Motion/TF50xx-NC/00_Base/AxPara
	- Allow write NC encoder calibration parameter 
	
- Fieldbus/EtherCAT/EcCoEReadNewestDiagMsg
	- Fixed byte shift to read details of message 

## [V3.1.2.0] - Release 2025-05-19

### Changed 
- StringHelper/getCntChatInStr + isStringNumeric
	- Renamed input variable Char to Chars 
	
- Moved generic analog FBs to own folder Analog

- Connectivity/TF6310-TcpServer
	- #Renamed TCPServerCtrl to TcpConnectionCtrl and moved FB, and as well as TCPSendRecCtrl and TcpSocketCtrl to new folder TcpBasic
	- Move UdpServerCtrl, UdpSocketCtrl and UdpSendRec to folder UpdBasic
	
- Connectivity/TF6340-SerialCom
	- Moved ComPortBackground and ComPortSendRec to new folder TcpBasic		

### Added
- DataBuffer/DoubleBuffer
	- Added output variables min and max time fill buffer
	
-IO/Cylinder/I_Cylinder	
	- Added more properties and methods to interface (isBusy,inError,isInBasePos,isInWorkPos,moveToWorkPos,moveToBasePos,noFeed)
	
- Logging/DataFileLogger and DataUdpLogger	
	- Added output variable MaxTimeSend/WriteData
	
- IO/Analog/
	- Added properties to access single bits of terminal status 
	- Added new FB AnalogInReal for new terminal series (EL37xx)

- IO/EL-EP/
	- Added FB for EL3681
	- Added FB for EL1262 (Input with Timestamp)
	- EL9x/Added FB for EL9501 (Power terminal with 0-20V output voltage and voltage/current inputs 
	
- Connectivity/TF6310-TcpServer/TcpBasic/TCPConnectionCtrl (Former TcpServerCtrl)
	- Added adapter link status check to FB to detect a lost network connection 
	- Added a second instance of ServerClientConnection to accept new connection requests and closing the old one at any time 

- Connectivity/TF6310-TcpServer/DeviceCom/New FBs TcpDeviceCom_SendRecBytes and TcpDeviceCom_SendRecString
	- FBs are useful to be used if the connected device works in handshake mode, where for any sent 'command' a response message of the connected device will be received
	- With pSrc or pDest variables set to 0, the FBs will work in only send or received mode 
	
- Connectivity/TF6310-TcpServer/DeviceCom/New FBs ComPortDeviceCom_SendRecBytes and ComPortDeviceCom_SendRecString
	- FBs are useful to be used if the connected device works in handshake mode, where for any sent 'command' a response message of the connected device will be received
	- With pSrc or pDest variables set to 0, the FBs will work in only send or received mode 
	
- Connectivity/TF6310-TcpServer/DeviceCom/New FBs ComPortEL6x22BEasyConnect 
	- FB provides and simple implementation for a serial communication via EL6xxx terminal in 22byte mode
	- The FB provides the 'handle' variable which is used to handover Tx/RxBuffer to FBs ComPortDeviceCom_SendRecBytes and ComPortDeviceCom_SendRecString
		
### Fixed
- '_Miscellaneous/SEQUENCE_HDL
	- Fixed tonOFF method 
	
- Connectivity/TF6310-TcpServer/TcpBasic/TCPServerCtrl 
	- Fixed cyclic call of create handle to avoid error in debug mode, keep Errors active until Enable was set to false
		
- Connectivity/TF6340-SerialCom/ComPortBasic/ComPortSendRec
	- Fixed repeated send or rec of packages which are handled in one PLC cycle
	
- Using local variable i in several properties to avoid issues when used attribute monitoring=call and other asynchron calls 
	
## [V3.1.1.1] - Release 2025-02-14

### Changed 
- Fixed typo break to brake throughout the project,
	- Output variable Q_Break from FB IOFcCom, changed to Q_Brake and will effect linked outputs!
	
- Logging/LogbookSubSysLog
	- Updated and improved FB default Syslog header is RFC 3164, new RFC 5454 can be enabled via options
	- Messages will be send after new interval or when buffer is filled... Several messages will be send within one frame 

### Added
- IO/Cylinder/FBs Cylinder and CylinderType4
	- Added new Input parameter PT_SensorDamping : TIME := T#0ms, to allow a damping of the sensor signal in case of flickering 

- IO/Drives/SoE/AxDriveSoE_Ax5000
	- Trigger read status after lock/unlock the brake to read actual status 
	
- Logging
	- Move FB DataFileLogger in folder Logging
	- Added new FB DataUdpLogger (streamer) to collect data via DoubleBuffer and send/stream packages out via Udp when buffer is filled 

### Fixed
- Motion/02_Options/Parameter
	- FB AxPara, correct PhysicalUnit to show °

## [V3.1.1.0] - Release 2024-10-10

### Changed 
- EventLogger/TriggerEvents/FB EventHandling, renamed variable Class to eClass to avoid future compiler error

### Added
- Statemodel/control
	- FB Statemodel.addSlave, added ads message if all slaves are already occupied

### Fixed
- Safety/Diag/
	- SafetyIODeviceDiag_wEvents, corrected DevTypeAndAddr for 2nd channel of AX5805 event

## [V3.1.0.18] - Release 2024-10-08

### Changed 
- _Miscellaneous/FB ERROR_HDL, renamed variable Class to EventClass to avoid future compiler error

### Added
- IO/EL-EP/
	- FB EL69xx added FSoEAddr as output variable
	
- IO/Drives/CoE/
	- Made AxDriveCoE FBs generic and DS402 conform 
	
- Fieldbus/EAP
	- FBs with default EAP IOs of adapter and publisher/subscriber variables
	
- _Miscellaneous/FB ERROR_HDL	
	- Added set method to set error, state, func and text,
	
### Fixed
- IO/Drives/CoE/
	- Updated CiA_DS402Controlword and CiA_DS402Statusword to be DS402 conform 

## [V3.1.0.17] - Release 2024-06-18

### Changed
- _Miscellaneous
	- Struct TC_VN_COLORS excluded from build to avoid TC_Vision lib 

### Added
- Motion/02_Options/Parameter
	- FB AxPara, added output variable for PhysicalUnit (°,mm,user)

### Fixed
- Motion/02_Options/Motion
	- FB AxHomningOnBlock updated to handle DS402 and MDP profile, new input variable to set used drive channel
- IO/Drives/CoE/
	- FB CiA_DS402Controlword, fixed command handling in method createControlword

## [V3.1.0.16] - Release 2024-05-27

### Changed

### Added
- FileHandling
	- Added File_Load function to FileHandling

### Fixed


## [V3.1.0.15] - Release 2024-04-16

### Changed

### Added

### Fixed
- Fieldbus/EtherCAT/
	- FB EcDiagBase fixed page fault if no of slaves is > MAX_SLAVES constant and FB gets triggered twice 
	
## [V3.1.0.14] - Release 2024-04-04

### Changed
- -IO/Drives/SoE
	- Added new (read) parameter P-0-0094-Configured Channel Peak Force to AxDriveSoE_Ax5000Param FB

### Added
- _Miscellaneous
	- Struct TC_VN_COLOR contains color codes based on TC_Vision Vector datatype
	
- Motion/TF50xx-NC/01_Main	
	- AdAdmin, added DriveAddress to VAR_OUTPUT

### Fixed
	
## [V3.1.0.13] - Release 2023-08-14
### Changed
- System/SystemInfo
	- UtcTimeXXX now based on Pc time (NT_GetTime())
	
### Added	
- System/SystemInfo
	- New output vars SysTimeFT, SysTimeSTRUCT based on FB GetSystemTime and updated within FB
	- New property, actDCTimeWithTimezoneBias showing DC actual time with timezone bias added
	
-IO/Drives
	-New FB AxDriveSoE_Ax5000CommutationCalib 
	
-IO/EL_EP
	-New FB AnalogOut_EL2535 
	
### Fixed
- Connectivity/ADS/AdsDataExchange	
	- Fixed, reset error not possible, if FB is disabled and no handle was created 
		
## [V3.1.0.12] - Release 2023-06-12
### Changed
- Fieldbus/EtherCAT/
	- FB EcDiagBase, added to trigger read diag if NoOfSlavesNOK > 0 too
	
### Added	
- Safety/Diag
	- New FB SafetyLogicAndIOTerminalDiag as extension of SafetyLogicTerminalDiag, which includes 8x inputs each for in module fault and and out module fault  
	- 	Added messages 7+8 for FSIN and FSOUT module fault to event logger 

### Fixed
- Motion	
 	-TF50xx-NC/00_Base/AxPara
		- seqWrite fixed len to write parameter SetMaxPosLagMonitoring

## [V3.1.0.11] - Release 2023-01-20
### Changed

### Added	

### Fixed
- IO/EL-EP/EL3356
	-  Added Super call to execute EcSlaveInfoDataExt

## [V3.1.0.10] - Release 2022-11-28
### Changed
- Connectivity/ADS
	- AdsDataExchange, set active to false each time after data were send 

### Added	


### Fixed
- Motion/TF5100-NCI/02_Options/RParameter
	- NCiReadWriteRParam, fixed type of pAddr from DWORD to PVOID to handle 64bit pointer

- GVL's
	- Param, corrected init value of constants PROFINET_DEVICE_DEV_IO_MAX_BOX to 1 and PROFINET_CONTROLLER_DEV_IO_MAX_BOX to 10
	
## [V3.1.0.9] - Release 2022-11-08
### Changed
- Fieldbus/Profinet
	- Changed Master and Slaves named FBs to Controller and Device 
	
- IO/EL-EP
	- FB EL3365, changed extend to EcSlaveInfoDataExt

### Added	


### Fixed
- IO/Drives
	- FB AxDriveBase, added Super(), to execute init of EcSlaveInfoDataExt
	- AxDriveXXXX FBs, added Super(), to execute AxDriveBase
	
- System
	- FB SystemInfo, fixed calculation of timezone bias for standard time and update timezone hourly to check for change
	
## [V3.1.0.8] - Release 2022-08-16

### Changed
- IO	
	- EcSlaveInfoDataEXT, added adsErrorLog if variables are not mapped (=0) or FB ReadBoxName ends with error 

- _Miscellaneous
	- ERROR_HDL.fnc STRING(20) changed to STRING() 
	- SeqHdl tonON, tonOff methods return value to show ton.Q status
	
- DataBuffer
	- Fifo+Ringbuffer changed datatype of variables count,idx etc. to UDINT
	

### Added	
- Statemodel/Control
	- FB Statemodel
		- Added method goToStopping
		- Added Set to property actState to enable modify the actual state from external if new option bit is set
		  Use with caution, writing set state might have unforeseeable side effects 
		  
- Struct with basic colors in TcVn Lreal array format 
- Helper function "nextIdx" to increment an index and report true until MaxIdx is reached

### Fixed
- StringHelper
	- isStringNumeric/isWStringNumeric returns FALSE if string is empty, will be true if e is included e.g. 9.9999992e-2

		
## [V3.1.0.7] - Release 2022-05-13

### Changed
- Motion	
	-TF50xx-NC/02_Options/Error
		- AxEventHandling, added AND NOT InTargetPosition for software limit errors to avoid error if axis target pos. was set to SW limit neg. or pos.
		
- StringHelper
	- HEXSTR_TO_D and LWORD, added check for x,X and # e.g. 0x0FA1 or 16#FFFB

- Motion	
 	-TF50xx-NC/02_Options/AxPara,
		- Removed SetEncScaling to match current NC-Settings, use SetEncScalingNumerator and SetEncScalingDenominator 
	
### Added	
- _Miscellaneous/Conversions
	- Added function ADSERROR_TO_HRESULT

- Motion	
 	-TF50xx-NC/00_Base/AxRWParaBase (Effects all read write param FBs inherited 
		- Add input bit EnableAutoInit BOOL := TRUE; Can be set to false to control init (read all parameter) by application 
		
### Fixed
- IO	
	-Cylinder/CylinderType4
		- Fixed issue with recursive call of method _readSensors 
		
- Motion	
 	-TF50xx-NC/02_Options/AxPara,
		- Fixed assignment of Numerator and Denominator in write function

## [V3.1.0.6] - Release 2022-01-11

### Changed	
- Motion	
	-TF50xx-NC/03_Utilities/AxStatemodel
		- Renamed variables Dec/Jerk to EmergencyDec/EmergencyJerk
		- Removed variable and function PT_DelEStopDisableAx
	
		
### Added	
- StringHelper
	- cutStrNumberToSeperator, the function cuts the left part until separator, in case the found characters are a valid number the value will be written into a LREAL IN_OUT_VAR
	
- Motion	
 	-TF50xx-NC/00_Base/AxParaCtrl 
		- To read/write NC ctrl parameter (Position and Velocity loop) 	
	-TF50xx-NC/03_Utilities/AxStatemodel
		- Variable ENDisableInAborting to disable the axis directly in aborting instead of executing MC_Stop with given emergency dynamics  
	
- Connectivity/ADS
	- AdsDataExchange - Added Ready variable to indicate FB created handle and is ready to start transmit 
### Fixed
- Motion	
	-TF50xx-NC/03_Utilities/AxStatemodel
		- Reset internal state state with every state change 
		
-FileHandling/Basic
		- Fb FileHandling, fixed declaration for FB to remove dir
		
## [V3.1.0.5] - Release 2021-11-02
-Tc build 4024.22

### Changed	
- Motion	
	-TF50xx-NC/00_Base/AxRWParaBase
		- Behavior of Execute and Busy/Done/Error signal flow if called via read/write(FALSE)
		
### Added	
	
### Fixed
- Motion	
	-TF50xx-NC/00_Base/AxRWParaBase
		- Set Error if deviceAddrIsValid is FALSE
		
## [V3.1.0.4] - Release 2021-05-19
-Tc build 4024.17

### Changed	
- IO	
	- AxDriveBase, changed EXTENDS to EcSlaveInfoDataEXT to have device name available for diagnostic...
	- EcSlaveInfoDataExt - changed variable "Name" to "DevName" to avoid collisions with "Name" variables of extended FBs (e.g. drives FBs)
	
- Fieldbus	
	- EtherCAT	
		- EcCoEReadNewestDiagMsg change length of message type to 64 bytes (0..63) 
	
- Motion	
	- TF50xx-NC
		- Moved "Motion" FB from AxNcBase to AxNcPTP so AcNcBase can be used for encoder axis 
		- Created new interface I_AcNcPTP extended from base to include the reference to "Motion"
		- Created AxNcPtpwJobs to include the job array function 
	-TF50xx-NC/01_Main/AxAdmin
		- Changed assignment of Busy to be TRUE during execution of internal MC_Reset,MC_Stop and MC_Power as long as MC_Power.Status is not TRUE
	-TF50xx-NC/03_Options/Parameter/AxPara
		- Fixed write index of parameter SetKv
		- Added parameter MaxPosLagFilterTime
		
### Added	
- Motion	
	-TF50xx-NC/01_Main/AxAdmin
		- get properties for isReseting (internal MC_Reset.busy) and isStopping (internal MC_Stop.busy)  
		
- Connectivity	
	-TF6340-SerialCom/ComPortSendRec
		- Options to get prefix, suffix removed from received string; new output variable LenRecData showing number of received bytes, characters
 	
### Fixed
-  Motion/02_Options/AxPara and IO/Drives/AxDrivexxxxParam
	- Set xxxRead(bExecute := FALSE) in any case to avoid a deadlock if FB read or write run into error

- StringHelper
	- Issue at INSERT_EXT where 1 of 1 insert was not executed 
	- Issue at DWORD_TO_XXXSTR_EXT where the separator was added to the end 
	
- IpcDiag
	- MDP_IpcDiag, changed input variable "NoOfFans" to "FanMask" to cover cases where two fans showing up, but only the second fan is installed 
	
- Logging	
	- LogbookSubWriteFile, fixed lost messages if new file would be created after day change
	

## [V3.1.0.3] - Release 2021-03-10

### Changed
- IpcDiag
	- Split FB for MDP Ipc Diag FB into read diagnoses (MDP_IpcDiag) and extension with Tc2Events (MDP_IpcDiag_wEvents)
		
### Added
- StringHelper 
	- function replaceUmlauts
	
- Motion	
	- TF511x-KIN/03_DUTs/Positions
		- New structs,Union and FB to represent kinematic positions 
		
- Logging
	- LogbookSubWriteFile, added function to write data and close file after time even if no file is opened
  	
### Fixed

## [V3.1.0.2] - Release 2020-11-03
- Checked with build 4024.12
- Marked as released
- Updated ET3rdPartyDevices to ET v3.1.0.2

### Changed
- Renamed _Miscellaneous/Conversions "ADSERRORID_TO_xxx" func. to "ADSERROR_TO_xxx"
- AxStepperDrive event type for warning from warning to message as warning will also signalled if drive is disabled for FW <=06

- Logging/
	- LogbookSubSendMail
		- Improved performance by implementing FB DoubleBuffer
	- LogbookSubSysLog
		- Improved performance by implementing FB DoubleBuffer
	- LogbookSubWriteFile
		- Added options OPTION_START_WITH_NEW_FILE to start with empty file in DELETE_MODE_DAILY if FB will be enabled or day changed
		- Improved performance by implementing FB DoubleBuffer

### Added
- DataBuffer
	- FB DoubleBuffer to record data in one buffer while the other (filled) part can be read or processed meanwhile
	- DB DataFileLogger as an extension to DoubleBuffer to write cyclic recorded data into file 

- IO 
	- New FBs for ELM terminals
		- AnalogInELMBase with base input vars (Min,MaxValue....),status word conversation and Ethercat slave info data 
		- AnalogInELMSingleSampleXXXX to read in and scale a single sample value (no oversampling....)
	
- IO/Drives/
	- DC/Ey73xx
		- New DC drive FBs AxDriveDC (wEvents) for EL73xx terminals
		
- _Miscellaneous/Conversions
	- Function getNoOfBits counts no of bits set to TRUE (32 := getNoOfBits(16#F0F0F0F0)))
	- Function setNoOfBits to set x numbers of bits in a LWORD variable (2#0000FFFF := TO_DWORD(setNoOfBits(16))
	- LWORD_TO_LREAL_EX function to convert and check a Double variable (words swapped) into Beckhoff REAL format
	- TO_FMLREAL to limit the number of digits in a real/lreal variable or convert a integer number into a LREAL variable with corresponding digits
		- e.g. REAL variable / 111.223 := TO_FMLREAL(111.223 , 4); while just REAL_TO_LREAL show a slightly different result -> 1111.2230224609375 := REAL_TO_LREAL(111.223); 
		- e.g. DINT variable / 111.223 := TO_FMLREAL(111223 , 4); 
	- Function LOGx(value,basis) to calculate a logarithm value with given basis x  
	  	
### Fixed
- AxDriveStepperParam, read request to wrong CoE object 
- AxDriveStepper_wEvents, avoid warning event if drive is disabled 
- Conversion functions HRESULT_TO_ADSERROR, ADSERROR_TO_WSERROR
- FB PartsPerTime flag trigger in method 
- AxDriveSoe_Ax5000wEvents reset Error and Errorid vars
- FB CylinderExt and CylinderType4 issue in overwritten method where Super call lead to page fault

## [V3.1.0.1] - Development 2020-10-05
- Marked as released
- Updated ET3rdPartyDevices to ET v3.1.0.1

### Changed
- Variable name "TotalCylceTime" to "ExecutionTime" in various FBs which shows the time the FB needed to finish 

- Fieldbus/EtherCAT
	- EcMasterIO
		- Changed some variable names and Frame information
	- EcDiagBase
		- Improved trigger for EcSlavesDiag
	- EcSlavesDiag
		-Handles hot connect groups and mixed bus sequence if connected HC groups are in a different layout then configured 
		-Improved InfoData list (array EC_SLAVE_DIAG_INFO_DATA) to include configured and scanned slave information as well as topology information 
	
### Added
- IO/Drives/
	- SoE
		- New FBs AxDriveSoE_Ax5000SwitchParamSet and AxDriveSoE_Ax5000CalcPower
		
### Fixed
- Event Ids of CANopenMasterDiag according to Eventlogger.xls config
- Quicksort FB

## [V3.1.0.0] - Development 2020-06-16
- Changed Company name from "Beckhoff Key Account Engineering" to "Beckhoff Electronics Mfg"
- Updated disclaimer
- Checked with build 4024.10 
- Create new empty lib <strong>"EngineeringToolboxLicDummy"</strong> as placeholder to overwrite chargeable licenses if not used 
- Moved FBs for 3rd party devices to new lib <strong>"ET3rdPartyDevices"</strong>

### Changed
- Folder structure  
	-Timing to TimeHelper
	-Move folder "Fieldbus" and "Safety" to root
	-IO folder structure
	-Moved "Drives" form motion to IO folder
	
- Renaming of variables, functions, FBs and data types
	- Naming convention: Variables and FB names starting with UpperCase, functions, properties and methods with lowerCase 
	- Variable names for Reset and Quit to ResetTrig and ConfirmTrig throughout the library 
	- Method names of methods Resetting and Quitting to reset and confirm throughout the library
	- Enums renamed to eXYZ 
	- Interface names changed to I_xxxx
	- All PLC_Open style FBs are inherited from "FbBase" 
	- Local IO variables renamed from e.g. _Status to Status
	
- Fieldbus/EtherCAT
	- Updated "EcMasterSupervisor" to include frame statistic and reset counter functionality 
	- Updated "EcSlaveSupervisor" to read slave CRC Error
	- Replaced "ExMasterDiag" by new FB "EcDiagBase_wEvents"
		
- Eventlogger
	- Improved FB "WriteEventsToLogbook" to catch every event
	- Timestamp format and name of Event logger entries at EventlogRead 
	
- Logging
	- Improved performance FB "LogbookPuplisher" and "LogbookWriteFile" (Cache data in one half of allocated memory, while the other half can be written to the file)
	- Renamed ads log functions to adslogXXXX and change parameter from LREAL to String for more flexibility 

- Separated core functions (e.g. EtherCAT, Safety diagnosis, Drives etc.) from "Eventlogger" and inherited from core FBs to fire events
	- (e.g. Read diag="AxDriveCoE" -> Fire events="AxDriveCoE<strong>_wEvents</strong>", in preparation to include Eventlogger2)

- IOs
	- Cylinder now includes an interface "I_Cylinder" inherited from "I_ActuatorWorkBase"
	- Ax Drives FBs inherited from new basis "AxDriveBase" incl. interface "I_AxDriveBase"
	- Ax Drives FBs with events (_wEvents) are inherited from core drive FBs like "Ax5000Soe_Ax5000" or "AxDriveCoE"
	- Motors - FBs now include interfaces ("I_AcutuatorOnOff" or "I_ActuatorFwdRev")
	- Moved FB "BlockEconomySmart" to new library <strong>"ET3rdPartyDevices"</strong>
	- FreqConv - Moved 3rd FBs to control 3rd party VFDs to new library ("EcFcComSEW, DS402 FBs for Danfoss, Lenze, Parker and Vacon. All are inherited form base "EcFcDS402_ComBase")
	
- Statemodel
	- Updated FB "Statemodel" to access slaves through interface pointer (Remote data will be changed via property)
	- Also a slave can actively add his reference to a master if the master reference gets assigned to the property "ipMasterUnit" of the salve (in case the ipSlaves array cannot be filled)
	- Renamed variables of FB "Statemodel", added new or changed methods and variable names, renamed enums 
	
- Safety 
	- Renamed SafetyIOTerminalDiag to "SafetyIOsDiag"
	- Replaced "SafetyIOTerminalDiagCtrl" to SafetyIODeviceDiagRead as one basic FB to read diag for all safety devices, EK1915, AX5x or new logic devices 
		Created "SafetyIODeviceDiag_wEvents" to trigger read diag information and fire events accordingly
	- Changed FB SafetyCircuitStatus to structure "SAFETY_CIRCUIT_STATUS" 

### Added
- Parameter to enable/disable AMS logger entries of FBs which are allocating memory from router memory pool (__NEW)
	- First allocation will be a hint: 'EngineeringToolbox | FB xxxx | An instance allocated %s bytes from the dynamic memory of the ADS router memory pool'
	- If the required memory space changed and additional memory will be allocated a warning will be displayed as previous memory stays allocated until PLC restart
	- {attribute 'monitoring' := 'call'} to several properties
	
- Miscellaneous
	- Conversion functions for Time struct and SYSTEMTIME formats (FILETIME_TO_TIME /FILETIME_TO_TIME_EXT / SYSTEMTIME_TO_DATE)
	
- Fieldbus/EtherCAT
	- FB to read newest message from terminal diag history ("EcCoEReadNewestDiagMsg")
	- New diag EtherCAT FB "EcSlavesDiag"	
		-Improved EtherCAT diagnostic and events (Shows list of found or scanned slaves, CRC error and state change counts in a list

- ControllerTools
	- SampleTime to SlidingAverage FBs 
	- "SlidingAverageExt" to allocate dynamic memory from router memory pool per parameter

- DataBuffer
	- "FifoBase" and "RingbufferBase" to inherit main FBs from that basis  

- IO	
	- FB to read or update FW of several terminals ("EcSlaveDevFWUpdater")
	- AX5000 parameter structs (Folder IO/Drives/SoE/Ax5000ParamSTRUCTs) 
	- CoE - Based FBs and enums for DS402 status and control word ("CiA_DS402Controlword"+"eCiA_DS402_CONTROL_CMD" and "CiA_DS402CStatusword"+"eCiA_DS402_STATUS_STATE") 
	- FB CylinderType4 with two base and two work pos sensors inherited from Cylinder  
	- FB CylinderExt with two status variables showing last runtime of a cylinder move
	- Several interfaces as templates for actuators e.g. "I_ActuatorFwdRev","I_ActuatorOpenClose","I_ActuatorStartStop" etc./-> see IO/_Interfaces 
		
- Motion
	-FB "AxNcPTP" incl. interface to represent basis axis (No drive, gear, statemodel or Job array)
		-Interface provides properties to access models via reference, (e.g. rAxisRef, rAdmin, rMotion etc...) 
	-FB "AxRWParaBase" as a basis FB for FBs to read and write NC or drive parameter ("AxPara", "AxDriveCoe_EL72xxParam", etc)
		-The FBs to read and write parameter can be project specific extended by inherit a project FB from the basis
		-By overwriting/extend the methods "seqRead/seqWrite" project specific parameter can be added
		
- Statemodel
	-Interface "I_Statemodel_Unit" to access base state model Fb via reference (rUnit)
	-Interface "I_StatemodelBase" to be used in actuators like cylinder 
	-Interface "I_Statemodel" for main "Statemodel" FB 
	
- Sysinfo 
	- to update timestamp timely if SetSysTime was used
	- var Timestamp3 as string converted from SYSTEMTIME_TO_STRING

### Fixed
- Handling of memory which will dynamically allocated by __NEW of FBs such as "FifoExt","RingbuggerExt","SlidingAverageExt" or "XmlReadWriteWithBackupFile"
	- New memory will only be allocated in case the required memory space increased - See also information about new library parameter under added 
	- Reason: Even the pointer to memory, which was allocated with  __NEW, will be deleted by DELETE, the memory will be stays allocated until system restarts 




	




