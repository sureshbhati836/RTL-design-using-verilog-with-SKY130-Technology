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

![132089629-c1380335-d442-4db1-86fa-3288b69615fd](https://user-images.githubusercontent.com/104729600/166183970-38fb5a58-75b2-4c4a-b88b-1efb0fdcafde.png)


fig: NetList File of Sub-modul
![image](https://user-images.githubusercontent.com/104729600/166184038-4d7bb7ce-fe03-4bf0-84a8-2bf87524d1e4.png)



# DAY 3 :

## LOGIC CIRCUITS OVERVIEW
Combinational and sequential logic circuits are the two types of digital logic circuits. Combinational circuits are a group of fundamental logic gates whose output is solely determined by the current inputs and do not require any clocks. They produce a basic circuit that can implement sophisticated logic using only logic gates. Sequential circuits are made up of flip-flops, which are memory elements. The output of the circuit is determined by both the current and previous inputs. The output requires clock inputs due to the existence of flip-flops. As a result, they produce a sophisticated circuit that can implement complex logic using memory.


1.) Combinational Logic Optimization Techniques

Logic optimization is a type of logic synthesis that aims to find an equivalent representation of a given logic circuit while adhering to one or more constraints. We perform to squeeze the logic and obtain the most optimal design, which can result in space and power savings. This can be accomplished using either the Constant Propagation Method (for example, Direct Optimization) or Boolean Logic Optimization (ex: K-Map or Quine-McCluskey Methods). The most optimal logic is attained in Constant Propogation by propogating the value of one input to the next step and all the way to the output. Synthesis tools use boolean algebra/K-map reductions to simplify difficult logic equations in Boolean Logic Optimization.

2.) Sequential Logic Optimization Techniques
The continuous propogation method is one of the most basic optimization techniques for sequential circuits. When the D input is tied low in a logic design, the Q pin of the flop should always have a constant value to optimise the sequential logic. Advanced strategies for obtaining a most condensed state machine include: 1) State Optimization, which optimises the underutilised states. 2) Cloning logic is performed during physical aware synthesis (where there may be a significant routing delay if two flops are located far apart). To avoid this, clone a flip flop with a lot of positive slack and meet the timing). 3) Re-timing - the combinational logic is efficiently partitioned to reduce the delay and hence increase the throughput.

## COMBINATIONAL LOGIC OPTIMIZATION

/Steps Followed for each of the optimization problems:
1. to view all optimization files
 (ls *opt_check*)
2. Invoke Yosys
( yosys)
3. Read library 
(read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib)
4. Read Design
(read_verilog opt_check.v)
5. Synthesize Design - this controls which module to synthesize
(synth -top opt_check)
6. To perform constant propogation optimization
 (opt_clean -purge)
7. Generate Netlist
( abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib)
8. Realizing Graphical Version of Logic for single modules
(show) 

fig : files for optimisation 

![Screenshot (900)](https://user-images.githubusercontent.com/104729600/166185136-0e0c67e7-8df1-4659-9a06-fa33303048f6.png)

### CASE 1: opt_check.v
fig : Expected logic from verilog file

![image](https://user-images.githubusercontent.com/104729600/166185205-3699ac61-c962-4fed-bc14-601245f7489a.png)

The value of y depends on a, y = ab.

for : Command for performing combinational optimization using constant propogation method.
![image](https://user-images.githubusercontent.com/104729600/166185289-d6471b79-8dd1-45ce-aff7-5ca14bcc9f24.png)


![image](https://user-images.githubusercontent.com/104729600/166186022-2f7d4de6-ff2c-4a22-bbe9-7873736bb66e.png)


fig : realisation of the logic after synthesis
![image](https://user-images.githubusercontent.com/104729600/166186049-8c3e129c-8f5c-4939-a191-aacad938c0d2.png)

The optimized graphical realization thus shows a 2-input AND gate being implemented

### CASE 2: opt_check2.v
image:  logic from verilog file

![image](https://user-images.githubusercontent.com/104729600/166186181-0e88c738-7b5f-49b8-a436-a5bff6b1bdb4.png)


the realised logic is , y = a+b.
fig : Realization of the Logic

![image](https://user-images.githubusercontent.com/104729600/166186262-87612793-8a5f-4067-8b52-7bbd4f29c63a.png)

As a result, the improved graphical realisation depicts the implementation of a 2-input OR gate. Although an OR gate can be implemented using NOR, this can result in a stacked PMOS architecture, which is not recommended for design. As a result, the OR gate is implemented using NAND and NOT gates (which has stacked NMOS configuration).

### CASE 3: opt_check3.v
fig : logic from verilog file

![image](https://user-images.githubusercontent.com/104729600/166186418-9267e3e9-0f97-47f3-b407-746f7c93e850.png)

the realised logic is y = abc.

fig : realisation after synthesis 
![image](https://user-images.githubusercontent.com/104729600/166186447-02bac336-8532-4b73-88f7-81cbb67f42db.png)

The optimized graphical realization thus shows 3-input AND gate being implemented.


### CASE 4: opt_check4.v

 fig :logic from verilog file
 
 ![image](https://user-images.githubusercontent.com/104729600/166186541-07437d6c-8446-4de8-943c-15fc34c340a2.png)
 
 the realised logic is y = a'c + ac.


![image](https://user-images.githubusercontent.com/104729600/166186632-135c5e1c-f825-4ad5-8ddc-c09725f52755.png)


the optimized graphical realization thus shows A XNOR C gate being implemented.



### CASE 5: multiple_module_opt.v

Due to the presence of multiple modules, the netlist was flattened before optimizing the logic circuit


fig :verilog file of top module
![image](https://user-images.githubusercontent.com/104729600/166186919-c17df916-0e8d-48a9-b11e-a2ce4c0c9b8a.png)


fig : Realization of the Logic

![image](https://user-images.githubusercontent.com/104729600/166186970-a4628f6c-b5b2-4e0b-a4a5-25728106f4da.png)


The optimized graphical realization thus shows a 2-input AND into first input of 2-input OR gate being implemented.


### CASE 6: multiple_module_opt2.v


fig : Verilog file

![image](https://user-images.githubusercontent.com/104729600/166187312-64ec25cc-dad5-45c6-8b42-e30924438419.png)

fig : Realization of the Logic


![image](https://user-images.githubusercontent.com/104729600/166187399-c589df47-a615-4e90-96ff-93464522e02a.png)


![image](https://user-images.githubusercontent.com/104729600/166187417-cfa5bd09-3449-49a9-9dd1-b1dbf8086a0f.png)


### SEQUENTIAL LOGIC OPTIMIZATION

/Steps Followed for each of the optimization problems:
1. To view all optimization files
(ls *df*const*)
2. To open multiple files 
(dff_const1.v -o dff_const2.v)
3. Performing Simulation
4. Load the design in iVerilog by giving the verilog and testbench file names
 (iverilog dff_const1.v tb_dff_const1.v) 
5.To dump the VCD file
(./a.out)
6. To load the VCD file in GTKwaveform
(gtkwave tb_dff_const1.vcd)
7.Performing Synthesis
8. Invoke Yosys 
(yosys)
9. Read library 
(read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd_-tt_025C_1v80.lib)
10. Read Design
(read_verilog dff_const1.v)
11. Synthesize Design - this controls which module to synthesize
(synth -top dff_const1)
12. There will be a separate flop library under a standard library

(dfflibmap -liberty ../my_lib/lib/sky130_fd_sc_hd_-tt_025C_1v80.lib)
13. Generate Netlist
( abc -liberty ../my_lib/lib/sky130_fd_sc_hd_-tt_025C_1v80.lib)
14. Realizing Graphical Version of Logic for single modules
( show )

### CASE 1: dff_const1.v
fig : logic from verilog file

![image](https://user-images.githubusercontent.com/104729600/166187921-67c97897-bee6-432e-b429-38e8e9d2c2a8.png)



Although Reset goes low, Q will wait for the clock to go high in order to become high. The flop will be inferred in this design.

fig : Verifying the Observation using Simulation

![image](https://user-images.githubusercontent.com/104729600/166188048-e63d72d3-35db-4468-9568-d45262639bfa.png)



fig : Statistics showing a flop inferred

![image](https://user-images.githubusercontent.com/104729600/166188088-47185412-0ed3-44ea-9a67-e8016a92aedc.png)


fig : Realization of the Logic

![image](https://user-images.githubusercontent.com/104729600/166188132-8e4ff1f8-d907-479e-901d-860939b847a3.png)

As a result, the inferred flip is visible in the optimised graphical realisation. In addition, the design code has a high level of activity.


### CASE 2: dff_const2.v

fig : logic from verilog file

![image](https://user-images.githubusercontent.com/104729600/166192433-1a21b3c3-cc4d-4b77-bc73-8f70c63ae21c.png)

fig : Verifying the Observation using Simulation

![image](https://user-images.githubusercontent.com/104729600/166192537-d66da1b5-6886-4abe-8740-526b66205e8f.png)

Q is constant with value of 1


fig : Statistics showing no flop inferred


![image](https://user-images.githubusercontent.com/104729600/166192693-b733970a-b54d-4ff6-bfe7-da3eb443c269.png)


fig : Graphical Realization of the Logic

![image](https://user-images.githubusercontent.com/104729600/166192797-a01146b2-b37b-4def-91a7-ae72dd3bcccf.png)

As a result, the optimised graphical realisation has no flop inferred and is a constant value of 1, regardless of the reset or clock signals.


### CASE 3: dff_const3.v

fig : logic from verilog file

![image](https://user-images.githubusercontent.com/104729600/166192857-0d61fc0b-5217-4e5c-990e-fa59bf8cd1ff.png)


There are two flips here; one is reset if the condition is Q, and the other is reset if the condition is D. With reset applied, Q1 waits for the next positive edge of the clock. Due to the TCK delay effect on the preceding flop, the subsequent flop will sample the value of 0. Except for one clock cycle, the output Q will always be high. Both flops should be present, and they will not be optimised.

fig : verifying the Observation using Simulation 

![image](https://user-images.githubusercontent.com/104729600/166194356-82893667-cfb7-4511-9c8d-f088e128096b.png)

fig : Statistics showing both flops being inferred


![image](https://user-images.githubusercontent.com/104729600/166194420-5b0eefe8-917a-493e-8ceb-d6813c1e6415.png)


fig : Realization of the Logic
![image](https://user-images.githubusercontent.com/104729600/166194479-57c1a390-38d2-433f-99fb-7467a076b245.png)

### CASE 4: dff_const4.v

fig :  logic from verilog file
![image](https://user-images.githubusercontent.com/104729600/166194541-c8742ccc-4a3d-4ad6-b6b4-1e1dac004f9b.png)

Because the output lines of both flops are constant 1, they are expected to be optimised. There will be no flops inferred from the generated netlist.

fig :  Observation using Simulation

![image](https://user-images.githubusercontent.com/104729600/166194818-206c2a7e-d132-4c62-9ed2-578d5edbdb78.png)

fig : showing no flops being inferred

![image](https://user-images.githubusercontent.com/104729600/166194866-2a79e86b-a4b5-48e7-a802-53cbe00c3ef0.png)

fig : Realization of the Logic after synthesis

![image](https://user-images.githubusercontent.com/104729600/166194941-bdd2a0d6-81e6-4e7a-8667-1826e6433898.png)


As a result, the optimised graphical realisation has no inferred flops and has a constant value of 1, regardless of the reset or clock signals.


### CASE 5: dff_const5.v

fig: logic from verilog file

![image](https://user-images.githubusercontent.com/104729600/166195101-2589be30-c9c4-4235-9c78-92846e6c86d6.png)

fig: Observation using Simulation

![image](https://user-images.githubusercontent.com/104729600/166195147-879219c5-c241-4383-ad70-1cd28a4630bb.png)

fig: Statistics 

![image](https://user-images.githubusercontent.com/104729600/166195197-f90c53d6-92e8-4e94-ba0a-e8003e92d007.png)


fig:  Realization of the Logic after synthesis

![image](https://user-images.githubusercontent.com/104729600/166195275-8b84113e-e287-4154-8409-dada754e5678.png)

The optimized graphical realization have the same flop inferred twice.



## SEQUENTIAL UNUSED OUTPUT OPTIMIZATION

//Steps Followed for each of the unused output optimization problems:
1. opening the file
( gvim counter_opt.v)
2. Invoke Yosys
 (yosys)
3. Read library 
( read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib)
4. Read Design
(read_verilog opt_check.v)
5. Synthesize Design - this controls which module to synthesize
( synth -top opt_check)
6. To perform constant propogation optimization
(opt_clean -purge)
7. Generate Netlist
(abc -liberty ../my_lib/lib/sky130_fd_sc_hd_-tt_025C_1v80.lib)
8.Realizing Graphical Version of Logic for single modules
( show )


### CASE 1: counter_opt.v
fig : logic from verilog file

![image](https://user-images.githubusercontent.com/104729600/166195694-a190aa2b-0139-4ef2-9e84-22696fd6a368.png)



![image](https://user-images.githubusercontent.com/104729600/166195712-7a199a04-874b-4e3f-bfe1-3b790c968307.png)


If the counter is reset, it is reset to 0, otherwise it is increased, similar to an upcounter. Because it's a three-bit signal, the counter resets after seven. However, because the final output q only senses the count [0], the bit toggles every clock cycle (000, 001, 010 ...111). The other two outputs aren't used, thus there's no output dependency. As a result, these unused outpus do not need to be included in the design.


fig : Statistics showing only one flop inferred instead of 3 flops sinces it is a 3 bit counter

![image](https://user-images.githubusercontent.com/104729600/166195891-e24d7631-a4b8-4a41-b69f-252f64aadb69.png)


fig: Realization of the Logic

![image](https://user-images.githubusercontent.com/104729600/166195932-1ed8556e-837c-4c2e-8e69-5b8a643811cf.png)

To accomplish the toggle function, the optimised graphical realisation output Q (count0) is sent to the NOT gate. The other outputs that do not rely on the primary output are turned off.


### CASE 2: counter_opt2.v


//Steps Followed:
1. Copying the code to a new file
2.  cp counter_opt.v counter_opt2.v
3.  gvim counter_opt2.v
4. Changes made in the verilog code, i for insert mode: 
5.  assign q = [count2:0] == 3'b100;

 fig : logic from verilog file

![image](https://user-images.githubusercontent.com/104729600/166196586-1ccae8bf-a21c-4ff5-b537-25ce89438de1.png)

Because all three bits of the counter are used in this scenario, the optimised netlist should have three flops.

fig :Statistics showing all three flops inferred


![image](https://user-images.githubusercontent.com/104729600/166196769-df20d5c2-9892-441f-b16f-72299da5bdc9.png)

fig : Graphical Realization of the Logic


![image](https://user-images.githubusercontent.com/104729600/166196820-0e929019-075f-4dac-889e-f97883f5c636.png)



All three flips are visible. Because incremental logic is required, the logic other than flops serves as the adder circuit. 
q = counter2.counter1'.counter0' is the output expression. As a result, all outputs that have no direct impact on the principal output will be optimised away.




# DAY 4

TOPICS COVERED
1.	GATE LEVEL SIMULATION
2.	SYNTHESIS SIMULATION MISMATCH
3.	EXPERIMENTS WITH GLS
4.	MISSING SENSITIVITY LIST
5.	CAVEATS IN BLOCKING ASSIGNMENTS

## 1.GATE LEVEL SIMULATION
#### What is GLS?

The design's functioning was tested using stimulus inputs, and the output was checked for compliance using a test bench module. The DUT was determined to be the RTL design (Design Under Test). The Netlist is referred to as the Design Under Test in Gate Level Simulation. The RTL code that was converted to Standard Cell Gates is logically the same as the Netlist. As a result, the test bench will be consistent with the design.


#### Advantages of GLS:

1. After Synthesis, logically test the design's accuracy.
2. Timing was not taken into account during the RTL Simulation. However, in actual applications, it is necessary to ensure that the design's time is met.


![image](https://user-images.githubusercontent.com/104729600/166197304-eb3f6254-4827-47a5-9d1f-00c67ba5be2a.png)

The meaning of the Netlist is given to the iVerilog using Gate Level Verilog Models, which are made up of all standard cells that have been instantiated. Verilog models at the gate level can be functional or timing aware. GLS can be used for timing validation as well as functional validation if the gate level models are delay annotated.


## 2. SYNTHESIS SIMULATION MISMATCH

What is the point of validating netlist's functioning if it is a real reciprocation of RTL? There could be a mismatch between synthesis and simulation for the following reasons:
1. Absence of Sensitivity List
2. Blocking Vs Non Blocking Assignments
3. Non Standard Verilog Coding


### 1. Absence of Sensitivity List:


module mux(
input i0,input i1
input sel,
output reg y
);
always @ (sel)
begin
   if (sel)
            y = i1;
   else 
            y = i0;          
end
endmodule


Simulator's output only changes when the input changes. When there is no action, the output is not evaluated. When the select is changing (when select is 1), the output is 1 when the input is 1 and 0 when the input is 0. The always block only evaluates when the choose pin transitions, and it is unaffected (the output does not reflect) by changes in the inputs 0 and 1.


Time	Logic
During Simulation	-----Logic acts as a Latch/Double edged Flop
During Synthesis	 -----Logic acts as a Mux

Corrected code for missing sensitivity list:

module mux(
input i0,input i1
input sel,
output reg y
);
always @ (*)
begin
   if (sel)
            y = i1;
   else 
            y = i0;        
end
endmodule



As a result, the mismatch is fixed by using always @ (*), in which the always block is evaluated whenever a signal changes. As a result, any changes in the inputs will be reflected in the output.


### 2. Blocking Vs Non Blocking Statments in Verilog:
CAVEAT 1:



When inside an always block, the problem always occurs. The statements in Blocking Statements are executed in the order that they are written. The first statement is always evaluated first, followed by the second (like a C program). The statements in Non-Blocking Statements are executed in parallel. Before being assigned to the left side, all assignments on the right side will be assessed.



Assignment	         Statement
  =	               Blocking Statment
  <=	              Non-Blocking Statment


module code (input clk,input reset,
input d,
output reg q);
always @ (posedge clk,posedge reset)
begin
if(reset)
begin
        q0 = 1'b0;
        q = 1'b0;
end
else
        q = q0;
        q0 = d;    
end
endmodule

the code will result in

![image](https://user-images.githubusercontent.com/104729600/166230075-3ca13cd7-3228-4921-8000-21373e5ed53c.png)


When two flops, like illustrated above, are combined, the code creates a shift register. The blocking statements are represented by the assignments within the code. Assigning 1 bit 0s to q0 and q results in an asynchronous reset connection. In the latter sections, however, q0 is allocated to q, and then d is assigned to q0. Let's say there's a modification in the code.


module code (input clk,input reset,
input d,
output reg q);
always @ (posedge clk,posedge reset)
begin
if(reset)
begin
        q0 = 1'b0;
        q = 1'b0;
end
else
        q0 = d;
        q = q0;    
end
endmodule


d is assigned to q0 in this scenario, and subsequently q0 is assigned to q. As a result, q0 has the value of d by the time the second statement is run. Only one flip will be implemented as a result of this. Previously, q had the value q0 and q0 had the value d, resulting in the use of two storage elements.

 ### 2. Usage of non-blocking statements


module code (input clk,input reset,
input d,
output reg q);
always @ (posedge clk,posedge reset)
begin
if(reset)
begin
        q0 <= 1'b0;
        q <= 1'b0;
end
else
        q0 <= d;
        q <= q0;   
end
endmodule


As a result, the order doesn't matter because RHS is evaluated first, followed by assignment. The presence of two flops, regardless of their order. When writing sequential circuits, always utilise non-blocking statements.

### CAVEAT 2: Causing Synthesis Simulation Mismatch

module code (input a,b,c
output reg y);
reg q0;
always @ (*)
begin
        y = q0 & c;
        q0 = a|b ;    
end 
endmodule



The code aims to generate a y = (A+B) function. C. Because there are blocking statements in the given code, they are evaluated in order when it enters always block. As a result, y is assessed first (q0.C), with q0 corresponding to the outcome of the preceding iteration. Only the second statement updates the q0 value.


Time	                         Logic
During Simulation           	Logic creates a delay or flop
During Synthesis	            Logic will not have a flop

When the order of the statements is changed: In this case, a OR b is evaluated first and the latest value is used for calculating y.



module code (input a,b,c
output reg y);
reg q0;
always @ (*)
begin
        q0 = a|b ;
        y = q0 & c;
end 
endmodule

As a result, it's critical to run the GLS on the netlist and compare the results to the specifications to verify there's no simulation synthesis mismatch.


### EXPERIMENTS WITH GLS

//Steps Followed: 
1. opening the file
( gvim ternary_operator_mux.v)
2. PERFORMING SIMULATION
3. Load the design in iVerilog by giving the verilog and testbench file names
( iverilog ternary_operator_mux.v tb_ternary_operator_mux.v)
4.To dump the VCD file
(./a.out)
5.To load the VCD file in GTKwaveform
(gtkwave tb_ternary_operator_mux.vcd)
6.PERFORMING SYNTHESIS
7.Invoke Yosys
(yosys)
8. Read library 
( read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib)
9. Read Design
(read_verilog ternary_operator_mux.v)
10. Synthesize Design - this controls which module to synthesize
(synth -top ternary_operator_mux)
11. Generate Netlist
( abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib)
12. Realizing Graphical Version of Logic for single modules
( show )
13. Write Verilog netlist
( write_verilog ternary_operator_mux_net.v)
14. PERFORMING GLS
15.Opening Verilog Models, Netlist and Test Bench
(iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/
sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v)
16.To dump the VCD file
(./a.out)
17. to load the VCD file in GTKwaveform
(gtkwave tb_ternary_operator_mux.vcd)

#### CASE 1: ternary_operator.v

it is the simplest method to define a 2 to 1   mux as the complexity increses it became more complex and unable to handle.

syntax :

 #### <Condition>?<True>:<False>
 
 ![image](https://user-images.githubusercontent.com/104729600/166231890-c674d6ac-0592-4b1d-a1af-0607dd3175fe.png)
 
 
 after simulation 
 
 
 ![image](https://user-images.githubusercontent.com/104729600/166232003-00d8af7d-ea93-444c-84db-3f378f448d54.png)

 fig : Statistics showing a flop inferred

 ![image](https://user-images.githubusercontent.com/104729600/166231917-2831805f-17dc-4fa8-9d53-79e915b75439.png)

fig : Realization of the Logic after synthesis
 
 
 ![image](https://user-images.githubusercontent.com/104729600/166232157-4077b126-73fc-4aa1-9f2d-d2c674cba703.png)

 O NAND gate with i1 and sel, inverted io, and Or to And invert gate with sel and inverted i0 as inputs. The expression = sel'.i0 + sel.i1 yields the output y.
 
 ![Screenshot (901)](https://user-images.githubusercontent.com/104729600/166234766-3e97009b-542b-4184-9c12-90da6053ddc0.png)

 
 fig : GLS Output
 
 ![image](https://user-images.githubusercontent.com/104729600/166234820-1c6bae46-a772-4652-94ff-5ee7740ec99c.png)

 
 ### MISSING SENSITIVITY LIST
 
 ##### CASE 2: bad_mux.v showing mismatch due to missing sensitivity list
 
fig :  Verilog file
 
 ![image](https://user-images.githubusercontent.com/104729600/166234934-bf6894ea-7c5c-4a75-b429-20f3ac59c53c.png)

 
 The sensitivity list contains only select input. So during Simulation, the logic acts as a latch and during synthesis, it acts as a mux.
 
 
 fig :Simulation Output
 
 
 ![image](https://user-images.githubusercontent.com/104729600/166235020-13e93ab7-b3b4-4c4f-834d-7ee1c1bf5579.png)

 
 When select is low, it is followed by i0, and the select line has no activity, therefore the output remains low. When the select is high, it follows i1, and the choose line is once again deactivated. As a result, it functions as a flip while maintaining its value.
 
 fig :Synthesis Statistics Report
 
 ![image](https://user-images.githubusercontent.com/104729600/166235168-9704c54f-2c4f-4521-85ea-87494f3f3588.png)

 Synthesis Output
 
 ![image](https://user-images.githubusercontent.com/104729600/166235285-c11e168d-88dc-485f-a288-194bc2c8a10c.png)

 
 There is a mux inferred during synthesis of the logic.
 
  fig : GLS Output
 
 ![image](https://user-images.githubusercontent.com/104729600/166235368-45bf32b5-f956-42b3-94bb-36961c0a8ab4.png)

 
 When the choose is low, the activity of input 0 is reflected on y, confirming the functionality of the 2x1 mux after synthesis. When the choose is high, the activity of input 1 is reflected on y as well. As a result of the missing sensitivity list, there is a synthesis simulation mismatch.
 
 
fig : Simulation Output
  
 ![image](https://user-images.githubusercontent.com/104729600/166235490-10060300-7e81-42b9-978d-fbe2261a19d5.png)

 (a+b) Equals d Therefore, if the inputs a,b are both 0, then a+b is also 0. d = 0 is the result. However, we notice the output d = 1 because it examines a previous value where a+b was 1.
 
 
 
fig :  Synthesis Statistics Report
 
 
 ![image](https://user-images.githubusercontent.com/104729600/166235596-0fe989c0-1b94-4376-85e8-12753d7b5dbe.png)

 
 
  fig  : logic Synthesis Output


 ![image](https://user-images.githubusercontent.com/104729600/166235652-3287727f-4ea7-4b2c-a52d-84c4109dcd6f.png)

 The synthesized design has or 2 and gate to realize the output
 
 
 fig : GLS Output
 
 
 ![image](https://user-images.githubusercontent.com/104729600/166235740-7550fcb5-a226-4e66-b782-59f21cd60e2d.png)

 
 For the identical set of input values, the value of output d is 0 after simulation and 1 after synthesis. As a result of the blocking assignments, there is a synthesis simulation mismatch.
 
 
 
# DAY 5
 
 	TOPICS COVERED
1.	IF STATEMENTS
2.	CASE STATEMENTS
3.	INCOMPLETE IF STATEMENTS
4.	INCOMPLETE CASE STATEMENTS
5.	STATEMENTS USING FOR
6.	STATEMENTS USING GENERATE
 
 
 ## 1. IF STATEMENTS
 
 Why IF Statements?

 The if statement is a conditional statement that determines which blocks of verilog code to execute based on boolean circumstances. It always comes out as Multiplexer. It's utilised for prioritisation logic and is always used inside the always block. A register should be assigned to the variable.
 
 Syntax for IF Statement
 
![Screenshot (906)](https://user-images.githubusercontent.com/104729600/166238332-969c2f16-5858-465b-b310-4d83a6550b50.png)

 
 Syntax for IF-ELSE-IF Statement


 
 hardware implementation 
 
 ![image](https://user-images.githubusercontent.com/104729600/166237354-3ab56f6d-d7b7-4c9f-80d4-664f938a1cfb.png)

 
 Condition 1 gets the highest Prority, If the condition1 is met - other conditions are not evaluated. LegN gets evaluated only if all the conditions precedding fail to meet.
 
 
### Cautions with using IF Statements
 
 Inferred latches might act as a 'warning sign,' indicating that the logic design isn't being implemented correctly. They indicate a faulty coding style that occurs as a result of missing or incomplete if statements/critical statements in the design. For example, if there is no else statement in the logic code, the hardware is unaware of the decision and will latch and attempt to hold the value. Unless the design functionality requires it, this style of design should be avoided (ex: Counter Design).
 
 
 ![image](https://user-images.githubusercontent.com/104729600/166238741-e9be729e-800d-4de5-a914-fe2dd7ca5426.png)

  ==>> Combinational circuits cannot have an inferred latch.
 
 
##  CASE STATEMENTS
 
 CASE Statements
 
 The hardware implementation is a Multiplexer. Similar to IF Statements, Case statements are also used inside always block and the variable should be a register variable.
 
 fig :Syntax
 
 ![Screenshot (908)](https://user-images.githubusercontent.com/104729600/166239074-637d02cc-8251-4a98-b092-0f25414f9073.png)

 
 ## Caveats in CASE Statements
 
 1. When a case statement is incomplete, it might be quite harmful. Inferred locks may be caused by structure. Code Case with default conditions to avoid inferred locks. If none of the circumstances are met, the code falls back to the default condition.
 
 ![Screenshot (909)](https://user-images.githubusercontent.com/104729600/166239345-df6b3cde-fad0-4912-bd9b-7d9bb0a79fe4.png)

 
2.  Partial Assignments in Case Statements – Values are not specified. Inferred latches will be created as a result of this. Assign all inputs in all segments of the case statement to avoid inferred latches.
 
 
 #### Comparison between If - Else If - Else If - Else Vs Case
 
 ![Screenshot (910)](https://user-images.githubusercontent.com/104729600/166239923-6c25319f-71f0-422a-8865-00459b392067.png)

 
 //Steps Followed for all the experiments: 
1. opening the file ( ls *incomp*)
( gvim *incomp* -o )
2. PERFORMING SIMULATION
3. Load the design in iVerilog by giving the verilog and testbench file names
(iverilog incomp_if.v tb_incomp_if.v)
4. To dump the VCD file
( ./a.out)
5. To load the VCD file in GTKwaveform
( gtkwave tb_incomp_if.vcd)
 
####  PERFORMING SYNTHESIS
1. Invoke Yosys
( yosys)
2. Read library 
(read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib)
3. Read Design
( read_verilog incomp_if.v)
4. Synthesize Design - this controls which module to synthesize
( synth -top incomp_if)
5. Generate Netlist
(abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib)
6. Realizing Graphical Version of Logic for single modules
(show) 
7. To write the netlist
( write_verilog -noattr incomp_if_net.v)
8. PERFORMING GLS
9. Opening Verilog Models, Netlist and Test Bench
(iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/
sky130_fd_sc_hd.v incomp_if_net.v tb_incomp_if.v)
10. To dump the VCD file
(./a.out)
11. To load the VCD file in GTKwaveform
( gtkwave tb_incomp_if.vcd)
 
 
 #### INCOMPLETE IF STATEMENTS
 
 ##### CASE 1: incomplete if statements
 
fig : Verilog file
 
 ![image](https://user-images.githubusercontent.com/104729600/166241121-a488d4f4-5d51-4d23-a338-f575ac466f8e.png)

 Else case is missing so there will be a D latch.
 
 
 fig : Simulation Output
 
 ![image](https://user-images.githubusercontent.com/104729600/166241206-31367aeb-1ae6-4bb0-80bd-2c9b283113ba.png)

  comment : When i0 (select line) is low, the output latches to a constant value. Presence of inferred latches due to incomplete if structure
 
 fig : Synthesis Statistics Report
 
 ![image](https://user-images.githubusercontent.com/104729600/166241310-e1e785a9-1ce6-4958-8e27-3dd1eb51a57b.png)

fig :  Synthesis Output

![image](https://user-images.githubusercontent.com/104729600/166241528-f19d0266-09df-49c8-85c5-3b8d09b60dd3.png)
 
 
 comment : The synthesized design has a D Latch inferred due to incomplete if structure (missing else statement).
 
 ### CASE 2: incomplete if statements

 fig: Verilog file
 
 ![image](https://user-images.githubusercontent.com/104729600/166241772-89f03102-e57a-49ff-946b-19314c6c3565.png)

observation :  Else case is missing so there will be a latch.
 
 fig : Simulation Output
 
 ![image](https://user-images.githubusercontent.com/104729600/166241933-81b28a72-81ef-4d23-8457-9548f61351c4.png)

 observation :
 When i0 is high, the output is determined by i1. The output latches to a constant value when i0 is low (when both i0 and i2 are 0). Because of the incomplete if construction, there are inferred latches.
 
 
 fig : Synthesis Statistics Report

![image](https://user-images.githubusercontent.com/104729600/166242176-f9a9e6e8-5590-45fa-8634-5513f02a65b6.png)

 
 fig : Synthesis Output
 
 ![image](https://user-images.githubusercontent.com/104729600/166242232-306a33fc-45bf-43ca-8c22-fa5da97d01b5.png)

 
 Due to an incomplete if structure, a D latch is inferred in the synthesised design (missing else statement).
 
 ####  INCOMPLETE CASE STATEMENTS
 
 CASE 1: incomplete case statements
 fig : Verilog file
 
 ![image](https://user-images.githubusercontent.com/104729600/166242459-406998ce-dccd-42ef-85b6-6e4f843ed99c.png)

 
 observation : There is an incomplete case structure, so a latch is expected.
 
 fig : Simulation Output
 
 ![image](https://user-images.githubusercontent.com/104729600/166242585-c0eb7f6a-23c9-46b1-8bf6-0c4e813b6bb8.png)

 
inspection :  When select signal is 00, the output follows i0 and is i1 when the select value is 01. Since the output is undefined for 10 and 11 values, the ouput latches to the previously available value.
 
 fig : Synthesis Statistics Report
 
 ![image](https://user-images.githubusercontent.com/104729600/166242978-6510f36c-201a-4be5-9151-60e814d9d663.png)

 
  fig : Synthesis Output
 
 ![image](https://user-images.githubusercontent.com/104729600/166243095-dcb8f846-7a5f-459d-bc35-0b85e8fe5f7c.png)

 The synthesized design has a D Latch inferred due to incomplete case structure (missing output definition for 2 of the select statements)
 
 #### CASE 2: incomplete case statements with default
 
 fig: Verilog file
 
 ![image](https://user-images.githubusercontent.com/104729600/166243240-ab718ad0-a014-401a-951a-75a9409ccf2b.png)

 
 obs : There is an incomplete case structure but with a default condition, so a latch is not expected.
 
 
 fig : Simulation Output 
 
 ![image](https://user-images.githubusercontent.com/104729600/166243348-a1777244-da92-4db5-b1f6-d6b9a31ffc66.png)

 
 When the select signal is 00, the output is i0, and when the select value is 01, the output is i1. The existence of default sets the output to i2 when the choose line is 10 or 11 because the output is undefined for these values. The output will not latch, and the circuit will not be a correct combination
 
 
 fig: Synthesis Statistics Report
 
 ![image](https://user-images.githubusercontent.com/104729600/166243499-000825c9-920b-4595-aada-c6cda4b27ec7.png)

 fig: Synthesis Output
 
 ![image](https://user-images.githubusercontent.com/104729600/166243562-d74a8d1c-de14-4de6-98d4-93643bd73505.png)

 obs : The synthesized design has combinational logic without latch due to the presence of default case statement
 
####  CASE 3: partial case statement
 
  fig :Verilog file
 
 ![image](https://user-images.githubusercontent.com/104729600/166243728-1be58e3f-bed9-47ee-aa3d-531232dbb9d0.png)

 
 here is a partial case structure with output of x undefined for one of the select values, so a latch is not expected.
 
 The mux for output y will not have a latch, while there will be a latch for mux with output x as one of the conditions is not defined
 
 ![Screenshot (911)](https://user-images.githubusercontent.com/104729600/166244190-f2f956c8-f539-4a67-a0cc-65d1bb0d5b45.png)

 fig : Synthesis Statistics Report
 
![image](https://user-images.githubusercontent.com/104729600/166244361-d727c457-5c8c-4d7a-a7e4-18035b8483ab.png)

 
 Synthesis Output
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
