ECE281_Lab4 : Datapath
===========

ALU Simulation Results:
![ALU] (https://raw.github.com/John-Rios/ECE281_Lab4/master/ALU_sim_Results.JPG)

Debugging for the ALU_shell.vhd file:
- 

Correct functionality?
- I am confident that my ALU vhd file is correct based on my simualtion results. The simulation results show the value of the OpSel function. The OpSel function defines how the ALU operates. The possible ALU operations are shown below. Based on the selected OpSel function, I knew what the result should be and could then compare the result from the simulation results to the expected result. My expected results matched my simulation results thus supporting my claim that my vhd file is properly coded. 

OpSel Functions:
--  OpSel : Function 
--  0     : AND
--  1     : NEG (2s complement)
--  2     : NOT (invert)
--  3     : ROR
--  4     : OR
--  5     : IN
--  6     : ADD
--  7     : LD
