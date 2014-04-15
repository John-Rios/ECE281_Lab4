ECE281_Lab4 : Datapath
===========
______________________________________________
ALU
-

ALU Simulation Results:
![ALU] (https://raw.github.com/John-Rios/ECE281_Lab4/master/ALU_Sim_Results.JPG)

Debugging for the ALU_shell.vhd file
- I ran into few errors while coding the vhd file. My largest issues simply came from struggling to remember how to code in VHDL. Initially, I attempted to code the ALUswitch process using conditional statements. This originally seemed easier but after coming across multiple syntax errors I discovered that I was less familiar with coding conditonal statements. Dr Neebel discussed with me that he believed case statements would be easier but helped me find an online source to assist me with the conditional format. After a few more minutes of sctruggling, I decided to adopt the case statement format. 
- After adopting the case statement format, I only ran into two syntax errors. The first was my definition of "others." Originally, I attempted to define all "other" cases as equal to "X." However, this did not work. To correct the error I deined all "others" as equal to "XXXX" because the variable is a 4 bit variable. My second error was my initial attempt at coding for the rotate right function. Originally, I attempted to use the ROR function. however, this did not work. Instead, I had to manually rotate each bit by making Result(0) equal to Accumulator(1) and so on. Each result bit was set equal to the the accumulator bit that is one bit higher. 

Correct functionality?
- I am confident that my ALU vhd file is correct based on my simualtion results. The OpSel function defines how the ALU operates. The possible ALU operations are shown below. Based on the selected OpSel function, which is shown in my simulation results, I knew what the result should equal based on the accumulator value and the data value. With the expected results known, I could then compare the expected results to the simulated results of the simulation results. My expected results matched my simulation results thus supporting my claim that my vhd file is properly coded. 

  OpSel Functions
  
  | OpSel | Function |
  |:-:|:-:|
  | 0 |	AND	|
  | 1	| NEG	|
  | 2	| NOT	|
  | 3	| ROR	|
  | 4	| OR | 
  | 5	| IN	|
  | 6 | ADD	|
  | 7 | LD |
  
___________________________________________________________________
Datapath
-
  
Datapath Simulation Results:
![ALU] (https://raw.github.com/John-Rios/ECE281_Lab4/master/DataPath_Sim_Results.JPG)
  
Datapath Simulation Results Using the Modified .wcfg File:
![ALU] (https://raw.github.com/John-Rios/ECE281_Lab4/master/DataPath_Sim_Modified.JPG)
  
Debugging for the Datapath.vhd File
- Initially, I struggled with this portion of the lab. Once I figured out how to code the Instruction Register, the rest of the coding came easily. I ran into two major errors during this section of the lab. The first was a syntax error that stated that I had an unexpected "IF" in my code. After 15 to 20 minutes of reading through my code and checking online, I decided to try and edit my If statements. I changed every instance of "else if" to "elsif". Suprisingly, this corrected the syntax problem I had run into. I learned there is a difference between "else if" amd "elsif." My second error was for my AeqZero function. Originally, I had tried to OR the NOT of each accumulator bit. This gave me the incorrect result. I changed the coding so that I took the NOT of all four accumulator bits added together rather than individually. This seemed to give me the correct results. 
  
Correct Functionality?
- To check my functionality, I compared my simulation results to the image of the correct simulation results provided in the lab. The first 50 ns of my results matched the first 50 ns of the correct results leading me to believe that I have completed this section of the lab correctly. 

_______________________________________________________________________
Reverse Engineering
-

Simulation Analysis: 

Datapath Simulation Results Using the Modified .wcfg File:
![ALU] (https://raw.github.com/John-Rios/ECE281_Lab4/master/DataPath_Sim_Modified.JPG)

Analysis:
- While attempting to conduct my analysis I ran into an error that stated "ERROR: at 106ns(10000): Iteration limit 10000 is reached. Possible zero delay oscillation detected where simulation can not advance in time because signals can not resolve to a stable value in File"C:/Users/C15john.Rios?Documents/ECE281/PRISM_Rios/Lab4/ALU_shell.vhd" Line 74. Please correct this code in order to advance past the current simulation time." The following was the line of bad code: "Result <= Data OR Accumulator;". I could not find an error with this line. I looked online, used the ISim help function, and simply attempted changing the code but was never successful in correcting the error. My simulation stopped at 106ns due to this error. I compared the code that was identified as troublesome to C2C Agnolutto's code but could not identify the problem. I am unsure if this is simply a bug or a coding error not related to the identified problem area. I spent hours attempting to solve this problem but was unsuccessful. 


- 0-15ns: Reset is low, so the active low nature of reset means that the program initializes everything to zero. IR is 0 meaning that we are ANDing the data and the accumulator. Data is unknown therfore the accumulator remains 0.
- 15-55ns: Reset becomes 1 and remains 1 for the duration of my simulation. This means reset no longer effects the program. IR equals 7 meaning we are loading a value. Data originally equals 7 but switches to B on the next clock cycle. We see B become loaded into the accumulator at 45ns.
- 55-85ns: IR equals 3 meaning we are rotating right. We take the value in the accumulator, which is 'B', and rotate this value right to get a value of 'D' in the accumulator. This is in fact what happens.
- 85-105: IR equals 5 meaning we are inputing a value. The value should load into the accumulator on the next clock cycle.
- 105-END: Error. My simulation would not proceed past 106ns, or the 10000 iteration. The ISIM stated that a WEBPACK license was not found. The following message displayed: "ERROR: at 106ns(10000): Iteration limit 10000 is reached. Possible zero delay oscillation detected where simulation can not advance in time because signals can not resolve to a stable value in File"C:/Users/C15john.Rios?Documents/ECE281/PRISM_Rios/Lab4/ALU_shell.vhd" Line 74. Please correct this code in order to advance past the current simulation time."
- 0-50ns: My code behaves as expected. The lab provides the description for this section of the simulation.
