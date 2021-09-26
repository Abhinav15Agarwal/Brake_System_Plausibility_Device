Please read this before operating BSPD V_2. 

This Circuit can be used for both CV and EV. This circuit is similar to FSG circuit with few changes. The major one is using 
the IRF9510 instead of si2309cds due to easily availability of former than latter. All the resistors used in this circuit are 1206 package and capacitor used are the 
ceramic capacitors.

1. The total comparators used in this circuit are 6 (U1,U2,U4).The IC used in this design is LM393M from TI.

2. The method we are using in this is the **Window Comparator**. Please read more about it on https://www.electronics-tutorials.ws/opamp/op-amp-comparator.html.

3. In U1:A the upper threshold is set at 1.6V with the help of voltage divider and at U1:B the lower threshold value is set at 0.45V.

4. Similar design is used at the IC U2.

5. Two LEDs are added at the output of the comparators to show the presence of the sensor value that maybe helpful for technical inspection.

6. Both the outputs of the the comparators are fed to the Logic NOR(SN74AHC1G02). Thus by getting the LOW(fault) at the both the inputs of the NOR gate fault is 
again read for 0.39sec using a RC timer circuit.

7. Again a comparator compares the output voltage of NOR with 3.5v at the non-inverting part(positive) of the opamp. If there is fault detected then the
voltage of the inverting part(negative) of the opamp will be more than that of the non-inverting this the output will be 0V.

8. If the voltage output of the opamp(U4:A) is LOW(0V), the PMOS(IRF9510) will we closed thus the pin of comparator(U4:B) at inverting part will be high
thus making the output of the comparator as LOW(0V).

9. Thus the output of the comparator U4:B will be LOW and thus the NMOS(BSS138) will be OFF hence will break the connection between SC_IN and SC_OUT.

10. The capacitor C7 and R20 are designed such a way that to produce a delay of 10 sec(5.6sec) for it to reset.

11. The transistor Q2 is used to reset the power once the fault is resetted.

 Sense_1 = Current Sensor output 
 Sense_2 = Brake Pressure Sensor Output
 SC_IN = Shutdown loop IN
 SC_OUT = Shutdown Loop OUT
 BSPD_FAULT = To LED on the DASH