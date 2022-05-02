# RTL-design-using-verilog-with-SKY130-Technology
it is a 5 day workshop on RTL design and synthesis.
![image](https://user-images.githubusercontent.com/104729600/166174861-7e8869b9-84bc-48f8-a27d-7ab79fd1b4da.png)


About the workshop 
A cloud-based workshop on verilog encoding directives, resulting in predictable logic in silicon. Workshop perspectives include: 
•	Digital logic design using verilog HDL.
•	Functionality validation of the design using functional simulation.
•	Creating testbenches to validate the functionality of the RTL design
•	Logic synthesis of functional RTL code

# TABLE OF CONTENTS
## day1
1)	Introduction to Verilog RTL Design and Synthesis
a)	Introduction to verilog rtl design and synthesis
b)	Introduction to the tools
c)	Block diagram of Design and test bench modules 
d)	Block diagram Simulation flow
e)	Environment setup
f)	Multiplexer 
g)	Good mux implementation using iverilog
h)	Gtkwave analysis
i)	Introduction to yosys and logic synthesis
j)	Design logic synthesis
## day2
2)	Timing Libs, Hierarchial Vs Flat Synthesis and Efficient Flop Coding Styles
a)	Understanding the library
b)	contents of the library file
c)	flat synthesis
d)	sub module level synthesis
e)	flip flop overview
f)	flip flop synthesis
g)	flip flop simulation
































# INTRODUCTION TO VERILOG RTL DESIGN AND SYNTHESIS

A low-level abstraction for representing a design circuit is the Register Tranfer Level. RTL design makes the design process easier for designers by automating it. It translates the functionality of a Hardware Description Languages (HDL)-written design circuit into similar combinational and sequential circuits. Fundamentally, Design is a set of Verilog codes that have intended functionalities to meet the standards. Simulating the RTL design ensures that it adheres to the specifications. A Simulator is used to verify or check the design, whereas a Testbench is used to apply stimuli to the design in order to test its functionality.

##	SKY130 - Sky130 process node and pdk(process design kit) are an open-source packages provided by Google and skywater for 130nm technology.
##	iverilog - Iverilog stands for Icarus verilog, is an open source verilog simulator.
##	GTKWave - GTKWave is an open-source vcd(value change dump) waveform viewer.
##	Yosys - Yosys is an open-source synthesis tool. These are the open-source tools used in the labs for the workshop.

##	BLOCK DIGRAM OF DESIGN AND TESTBENCH MODULES
![Screenshot (893)](https://user-images.githubusercontent.com/104729600/166175295-d16caaf5-e3ed-41a9-b22c-665860030e65.png)

Design module may have one or more primary inputs and primary outputs. However, testbench will not have any primary input or output.

![Screenshot (894)](https://user-images.githubusercontent.com/104729600/166175370-b8ed6850-67ed-4dc3-9454-a0b76e982db7.png)



##	ENVIRONMENT SETUP
•	#Steps Followed:
•	//create a directory
•	$ mkdir VLSI 
•	//Git Clone vsdflow. 

The sky130RTLDesignAndSynthesisWorkshop Directory contains the following files: My Lib - which contains all of the necessary library files; lib - which contains all of the standard cell libraries to be used in synthesis; and verilog model - which contains all of the standard cell verilog models for the standard cells in the lib. All of the experiments for lab sessions are stored in the verilog files folder, which includes both verilog and test bench code.

![image](https://user-images.githubusercontent.com/104729600/166175402-81462c4f-4122-4dd4-8d51-194f5656b3f4.png)


##	GOOD MUX IMPLEMENTATION USING IVERILOG

 2-to-1 multiplexer consists of two inputs D0 and D1, one select input S and one output Y. Depending on the select signal, the output is connected to either of the inputs. Since there are two input signals, only two ways are possible to connect the inputs to the outputs, so one select is needed to do these operations.
 
 ![Screenshot (895)](https://user-images.githubusercontent.com/104729600/166175536-e8b976b2-dcef-4540-8c88-fd43b7c57322.png)
 
 #Steps Followed:
•	Load the design in iVerilog by giving the verilog and testbench file names
•	iverilog good_mux.v tb_good_mux.v 
•	List so as to ensure that it has been added to the simulator
•	 ls
•	To dump the VCD file
•	./a.out
•	To load the VCD file in GTKwaveform
•	gtkwave tb_good_mux.vcd

![image](https://user-images.githubusercontent.com/104729600/166175569-14b7888d-8f62-44e7-9666-f5a16b404718.png)

![image](https://user-images.githubusercontent.com/104729600/166175582-0af18d89-76a0-479a-ab8e-acc7d45f807b.png)


•	GTKWave is the waveform analyzer and is the primary tool used for visualization and thereby to check the design functionality.

##	INTRODUCTION TO YOSYS AND LOGIC SYNTHESIS
The tool Synthesizer (Yosys) is used to convert RTL to netlist. The netlist is a common cell-based representation of the design (in the form of the cells present in the .lib). The design and the netlist file should be same. The optimization stage of the CAD process, where the RTL code is turned into a netlist, is known as logic synthesis. The stimulus should be the same as the RTL simulation's output. The code for the design was written in Verilog, and the usual cell format of the code is netlist. Between the RTL design and the synthesised netlist, the fundamental inputs and outputs will be the same. It means that we can use the same testbench that we used for RTL design.


![Screenshot (896)](https://user-images.githubusercontent.com/104729600/166175646-6a857915-7536-4582-94a9-191b9a61b213.png)

## Synthesis of Logic
The behavioural representation in HDL form for the needed specification is known as RTL Design.The design is transformed into gates, and the interconnections between the gates are created. This is distributed in the form of a file called netlist. To get the netlist file, we mix the RTL design with.lib and synthesise it.

•	.lib file is a collection of logical modules which includes all basic logic gates. It may also contain different flavors of the same gate (2 input AND, 3 input AND – slow, medium and fast version).
                        
![Screenshot (897)](https://user-images.githubusercontent.com/104729600/166175730-54835699-d50e-4d61-a92d-1386f5371b4c.png)

## 	DESIGN LOGIC SYNTHESIS
Steps Followed:
1)	Invoke Yosys
2)	yosys
3)	Read library 
4)	read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__t_025C_1v80.lib
5)	Read Design
6)	read_verilog good_mux.v
7)	Synthesize Design
8)	synth -top good_mux
9)	Generate Netlist
10)	abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
11)	Realizing Graphical Version of Logic
12)	show
13)	Writing the netlist 
14)	write_verilog -noattr good_mux_netlist.v

FIG: Steps for Design Synthesis
![image](https://user-images.githubusercontent.com/104729600/166175798-856d4fc3-647f-4ba4-bebc-c152ceff5dea.png)

FIG: Graphical Representation of the Logic using show commanD
![image](https://user-images.githubusercontent.com/104729600/166175843-cf1ba9b0-8534-4b72-8310-f3c93eb8d99b.png)

![image](https://user-images.githubusercontent.com/104729600/166175861-4d41ca91-f0a8-4cbc-ac57-17c092115bc3.png)

FIG: Writing the Netlist
![image](https://user-images.githubusercontent.com/104729600/166175892-6013bfa8-5d6a-45bf-babb-0351c37ce75b.png)


## THE LIBRARY
Process (Variations due to Fabrications), Voltage (Changes in the behaviour of the circuit), and Temperature are three critical parameters that govern how Silicon functions in a design (Sensitivity of semiconductors). To model these variations, libraries are characterised.

1)	Steps Followed:
2)	Command to open the libary file
3)	gvim ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
4)	To shut off the background colors/ syntax off:
5)	 syn off
sky130_fd_sc_hd__tt_025C_1v80.lib


PARAMETERS	MEANING
SKY130	Technology - CMOS
fd	Foundary - Skywater
sc	Standard Cell - Digital
hd	Density - High
tt	Process - Typical
025C	Temperature - Measure
1v80	Voltage - Measure

## HIERARCHICAL SYNTHESIS
Steps Followed:
1)	gvim multiple_modules.v
2)	Yosys
3)	read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
4)	read_verilog multiple_modules.v
5)	synth -top multiple_modules
//Generate Netlist
6)	abc -liberty ../my_lib/lib/sky130_fd_sc_hd__t_025C_1v80.lib
//Realizing Graphical Version of Logic for multiple modules
7)	show multiple_modules
//Writing the netlist 
8)	write_verilog -noattr multiple_modules_hier.v
9)	!gvim multiple_modules_hier.v

![Screenshot (898)](https://user-images.githubusercontent.com/104729600/166176010-e5084c4d-8b08-4e69-a071-aebd7b289bc0.png)


•	GENERETED NETLIST BY YOSYS

![image](https://user-images.githubusercontent.com/104729600/166176045-2a937e6f-19c4-4895-9cbc-f3d8d894f4ff.png)

###	MULTIPLE MODULES IN GTKWAVE
![image](https://user-images.githubusercontent.com/104729600/166176109-9e03c0b1-ce46-46ee-8253-06817fa8aa3a.png)

SYNTHESIS

![image](https://user-images.githubusercontent.com/104729600/166176132-7761f3b5-d741-47c5-a544-bcb696f1393e.png)

##	FLAT SYNTHESIS
Steps Followed:
//To flatten the netlist
•	flatten
//Writing the netlist in a crisp manner and to view it
•	write_verilog -noattr multiple_modules_flat.v
•	!gvim multiple_modules_flat.v

![image](https://user-images.githubusercontent.com/104729600/166176174-84637c47-9e0b-4071-ac66-af9933336014.png)

•	SUB MODULE LEVEL SYNTHESIS

When there are several instances of the same module, sub-module level synthesis is favoured. In terms of time, sythesizing the same module multiple times may not be advantageous. Instead, synthesising one module, replicating its netlist, and stitching it together in the top module can be done. This is especially useful in large-scale designs that employ the divide-and-conquer strategy

Steps Followed:
//Invoke Yosys
o	yosys
//Read library 
o	read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd_-tt_025C_1v80.lib
//Read Design
o	read_verilog multiple_modules.v
//Synthesize Design - this controls which module to synthesize
o	synth -top sub_module1
//Generate Netlist
o	abc -liberty ../my_lib/lib/sky130_fd_sc_hd_-tt_025C_1v80.lib
//Realizing Graphical Version of Logic for single modules
o	show 
//Writing the netlist 
o	write_verilog -noattr multiple_modules_hier.v
o	!gvim multiple_modules_hier.v

SUBMODULE REALIAZATION OF SUBMODULE

![image](https://user-images.githubusercontent.com/104729600/166176270-ef1a277d-1c3a-4c7d-b6ed-642ae91b1076.png)

Statistics of Sub-module
![image](https://user-images.githubusercontent.com/104729600/166176307-3e7988dd-218d-4119-a338-f1da5b2580da.png)
 fig :NetList File of Sub-module
![image](https://user-images.githubusercontent.com/104729600/166176341-bdb9a152-fbcf-474b-8d66-0bf1c05f049e.png)

##FLIP FLOP OVERVIEW
When an input signal changes state in a digital design, the output signal changes after a propagation delay. Singals are delayed by all logic gates. These delays generate expected and unwanted transitions in the output, known as Glitches, in which the output value differs from the predicted value for a brief period of time. When the signals are merged at the output gate, an increase in delay on one line can produce a glitch. In other words, more combinational circuits result in more glitchy outputs that do not settle with the output value.there is a need to store the values called as flop elements. D Flip-flops (aka Data or Delay Flip Flops) are the widely storage elements used to restrict the glitches.

![image](https://user-images.githubusercontent.com/104729600/166182674-4a6a6a59-e040-4acd-b985-3de6dab55845.png)

Flop elements hold a single bit of data and can be in one of two states: 0 or 1. They're sandwiched between the combinational circuits, and the output of the flop changes as the clock edge approaches. Although the input is erratic, the outcome is consistent. As a result, the next combinational circuit will get a stable input, and its output will be predictable and stable.

 RTL codeing of a Flip Flop:
Every flop element needs an initial state, else the combinational circuit will evaluate to a garbage value. In order to achieve this, there are control pins in the flop namely: Set and Reset which can either be Synchronous or Asynchronous.

### Asynchronous Reset/Set:

![image](https://user-images.githubusercontent.com/104729600/166182756-8a4c8889-0ae2-4f47-a467-8b03d587c695.png)

![image](https://user-images.githubusercontent.com/104729600/166182778-f3c061be-9342-4947-abcc-d4e0a4b994bd.png)

When there is a change in the clock or the set/reset, the always block is evaluated. The circuit is sensitive to the clock's positive edge. The singal q line changes as the signal goes low/high, depending on the reset or set control. As a result, it does not occur on the clock's positive edge and occurs regardless of the time.

### Synchronous Reset:
![image](https://user-images.githubusercontent.com/104729600/166182833-0246c1b4-75a6-496e-8ba7-bd65064636c0.png)

The singal is always waiting for the clock and is set to the D Pin of the flop. The D pin will wait for the clock's positive edge, and if it occurs, the output will alter accordingly. Only posedge clk is included in the sensitivity list.

### Both Synchronous and Asynchronous Reset:

![image](https://user-images.githubusercontent.com/104729600/166182890-48be43e1-fba4-4213-8170-c1034a4b2891.png)

When utilising the Set and Reset control pins, use caution as they may cause race circumstances. The always block is checked for the clock's positive edge and asynchronous reset. The use of else if means that the always block has been assessed due to the clock's positive edge.

FLIP FLOP SIMULATION
#Steps Followed for analysing Asynchronous behavior:
1. Load the design in iVerilog by giving the verilog and testbench file names
       ( iverilog dff_asyncres.v tb_dff_asyncres.v) 
2. List so as to ensure that it has been added to the simulator
( ls)
3. To dump the VCD file
(./a.out)
4. To load the VCD file in GTKwaveform
( gtkwave tb_dff_asyncres.vcd)


 Behavior of DFF with Asynchronous Reset using gtkwave
![image](https://user-images.githubusercontent.com/104729600/166183022-b8194604-67e2-40d8-8b34-ed3f5d9238ad.png)

Observation: The output does not pause to wait for the clock to strike (independent of positive edge of the clock).

### FLIP FLOP SIMULATION

//Steps Followed:
1. Invoke Yosys
     (yosys)
2. Read library 
(read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib)
3. Read Design
(read_verilog dff_asyncres.v)
4. Synthesize Design - this controls which module to synthesize
( synth -top dff_asyncres)
5. there will be a separate flop library under a standard library

( dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib)
6. Generate Netlist
( abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib)
7. Realizing Graphical Version of Logic for single modules
 (show) 
8. Writing the netlist in a crisp manner 
( write_verilog -noattr dff_asyncres_ff.v)
(!gvim dff_asyncres_ff.v)

fig : Statistics of D FLipflop with Asynchronous Reset
![image](https://user-images.githubusercontent.com/104729600/166183291-d684d89a-1ed8-4cc3-8604-94e8ef0f2932.png)

fig :Realization of the Logic
![image](https://user-images.githubusercontent.com/104729600/166183324-33905a06-15b4-4469-92ae-25b8419713d1.png)

fig: NetList File of D FLipflop with Asynchronous Reset
![image](https://user-images.githubusercontent.com/104729600/166183350-67efdcae-5b84-433b-b41b-6b1781c43ba1.png)

## OPTIMIZATION TECHNIQUES
//Steps Followed:
1. modules used for this experiment are opened using the command    (gvim mult_*.v -o)
2. invoke Yosys
     (yosys)
3. Read library 
  (read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib)
4. Read Design
 (read_verilog mult_2.v)
5. Synthesize Design - this controls which module to synthesize
(synth -top mult_2)
6. Generate Netlist
(abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib)
7. Realizing Graphical Version of Logic for single modules
( show )
8.Writing the netlist in a crisp manner 
(write_verilog -noattr mult_2.v)
(!gvim mult_2.v)

CASE 1: mult_2.v
Mul2: It takes a three-bit input and produces a four-bit output. The output has a connection that is double that of the input. The output appears to be the same as the input, but with zeros appended. In an ideal world, no hardware is required without the use of a multiplier.
fig : Expected logic from RTL file

![image](https://user-images.githubusercontent.com/104729600/166183598-0d793bf5-9465-45a2-8b77-fa8229b0d261.png)

fig: Statistics of D FLipflop with Asynchronous Reset

![image](https://user-images.githubusercontent.com/104729600/166183627-8732bfb0-7c08-4ddb-9447-e713e96ede6c.png)


after optimisation No hardware requirements - No # of memories, memory bites, processes and cells. Number of cells inferred is 0.

abc command return due to absence of standard cell library
![image](https://user-images.githubusercontent.com/104729600/166183657-e4f29cc7-1b5d-4266-9cfd-6d65a2ea9296.png)



fig : Realization of the Logic after synthesis

![image](https://user-images.githubusercontent.com/104729600/166183759-bbeedf1f-1f6d-428e-a130-83114286e997.png)