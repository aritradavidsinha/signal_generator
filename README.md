This repository contains the files by which we have developed a signal generator at variable frequency using TIVA Launchpad and a LTC1661 ADC.
The description and demonstration of the project can be found can be found at http://shukra.dese.iisc.ernet.in/edwiki/Signal_Generator_using_TIVA_microcontroller_-_2018.
Amongst the include files the tm4c123gh6pm.h contains the definitions of the register macros(like GPIO_PORTB_DATA_R,etc.), while Waveforms.h contains the Look-Up tables for 4 different types of waves. The idea is to send each of the values from the LUT to the ADC, so that at the output of ADC, the corresponding waveform is generated. Each waveform is generated by 120 samples stored in the LUT. SW2 is used to change the waveform type.
SW1 modifies the delay between two consecutive values of the LUT being sent out-in other words, this switch modifies the frequency of our waveform. For this purpose, we have used a 32 us block(because of the settling time required by the ADC). For a frequency f, the 32 us block has to be called for approximately 100000/(96*f) times between two consecutive LUT values. When SW1 is pressed, f increases by 10 and the actual waveform frequency increases by almost 6 Hz(as seen on  an oscilloscope) at low frequencies. As you might notice, this does give uniform increment in frequency at all ranges-because although the aforementioned division may return floats, the loop of 32us block can only be run an integral number of times. For example, if the f is 150, the loop runs for 6 times as the result of the division is 6.94- after pressing SW1, the value of f becomes 160, but the loop runs for 6 times only as the result of the division is 6.51; thus, the waveform frequency effectively remains unchanged. 
