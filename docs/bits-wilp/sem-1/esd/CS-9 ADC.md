# CS-9 ADC

## 1:39:30 Opens the ADC Project
## 1:44:05 Starts Debugging
## 1:44:20 How to see UART Window for Output
Serial Windows  
UART #1  
## 1:45:34 How to give ADC input
## 1:48:18 How to give Temperature as input to ADC

## Logic Analyzer Setup
Add `portc`.

## Other Notes from STM32F103xx Reference Manual.pdf
### Reading the temperature  (Page 236)
To use the sensor:  
1. Select the ADCx_IN16 input channel.  
2. Select a sample time of 17.1 µs  
3. Set the TSVREFE bit in the ADC control register 2 (ADC_CR2) to wake up the  
temperature sensor from power down mode.  
4. Start the ADC conversion by setting the ADON bit (or by external trigger).  
5. Read the resulting VSENSE data in the ADC data register  
6. Obtain the temperature using the following formula:  


<center>Temperature (in °C) = {(V<sub>25</sub> - V<sub>SENSE</sub>) / Avg_Slope} + 25</center>

Where,  

- V<sub>25</sub> = V<sub>SENSE</sub> value for 25° C and  
- Avg_Slope = Average Slope for curve between Temperature vs. V<sub>SENSE</sub> (given in  
mV/° C or µV/ °C).  

Refer to the Electrical characteristics section for the actual values of V<sub>25</sub> and  
Avg_Slope.

## From Electrical characteristics section of stm32f103rb.pdf (Datasheet)
### Temperature sensor characteristics (Page 78)

- Avg_Slope = 4.3 mV / °C (Typical)
- V<sub>25</sub> = 1.43 V (Typical)

## Other nice references for coding:

- https://community.st.com/s/question/0D50X0000BbMopqSQC/stm32-internal-adc-for-reading-temperature