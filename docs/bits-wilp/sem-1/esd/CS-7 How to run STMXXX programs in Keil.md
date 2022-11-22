# CS7 - How to run STMXXX programs in Keil

## Contact Session Video
https://youtu.be/aKojE6QmyQk

## Installing the STM32F103RB Board into Keil
Open `Pack Installer`  
Go to the `Boards` tab  
Search for `STM32F103RB`  
Select `NUCLEO-F103RB`  
Go to the `Packs` tab  
Under `Device Specific` → `Keil::STM32F1xx_DFP` → `Install`   

## 07:54 Project Creation
Project → New uVision Project → Give a name and Save  

## 08:41 Project Creation contd.
Software Packs → `STM32F103RB` → OK  
Device → Startup  
CMSIS → Core  
OK  

## 12:28 Setup Debugger
`Options for Target`  
`Target` → Xtal: 8.0
`Target` → Enable `Use MicroLIB`  
`Linker` → Enable `Use Memory Layout from Target Dialog`  
`Debug` → Use Simulator  
`Dialog DLL`= `DARMSTM.DLL`  
`Parameter`= `-pSTM32F103RB`  

## 19:35
Something about peripheral clocks

## 33:09
How to debug
Peripherals → General Purpose I/O → GPIOA