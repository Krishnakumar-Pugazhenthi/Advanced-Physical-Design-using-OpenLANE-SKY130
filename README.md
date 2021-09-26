# Advanced-Physical-Design-using-OpenLANE-SKY130
#  ADVANCED PHYSICAL DESIGN USING OpenLANE/SKY 130


 **WORKSHOP(Sept 22- Sept 26)**
## Table of Contents

 
## *Day1-Inception of Open-source EDA, OpenLANE and SKY130 PDK*

Pads-->Signals are sent and recieved from outside the chips through pads
Macros-->Digital Logic blocks such as RISCV SoC and SPI.
Foundry-->Places where chips are manufactured.
Foundry IP's-->Manually designed blocks such asPLL,SRAM,ADC and DAC 

**Process Design Kit (PDK)**
It acts as an interface between the Designer and the fabrication.It consists of files to model a fabrication. It contains Device models, DRC and LVS rules, Input output Library and Standard Cell Libraries. SkyWater 130nm PDK's are used for the entire workshop.

An ASIC chip can be designed with an RTL IP, EDA tool and an PDK kit.
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY1/asic_flow.jpg)

OPENLANE 
Openlane creates an automated GDSII file.The openlane automates from RTL synthesis stage till verification after which a GDSII file is created. GDSII file contains the entire design architecture such as memory, design , IP's in a binary file format.

![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY1/openlane_flow.jpg)

Invoke the docker to open OpenLANE
```
/Desktop/work/tools/openlane_working_dir/openlane$ docker
```
The follwing command is to open it in an interactive mode where we can execute in a step by step manner.
```
bash-4.2$ ./flow.tcl -interactive
```
Import the required packages 

``
package require openlane 0.9
``

![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY1/openlane%20start.jpg)

Design preparation

    prep design picorv32a

![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY1/prep%20design.jpg)


![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY1/picorv32a.jpg)

Runs directory is created under Picorv32a 
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY1/runscreated.jpg)

Variables Requried
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY1/variable_required.jpg)

**SYNTHESIS**

OpenLane Tools for Synthesis
 -   `Yosys` - Performs RTL synthesis
 - `abc` - Performs technology mapping
 - `OpenSTA` - Performs static timing analysis on the resulting netlist to generate timing reports
 
Synthesis Variables
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY1/synthesis_variable.jpg)
```
run_synthesis
```
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY1/synthesis.jpg)

Synthesis file
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY1/synthesisfile.jpg)


Flop Ratio--> Total Number of Flops/Total Number of Cells

No of Cells
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY1/no_of%20Cells.jpg)
No of flops
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY1/dflipflop.jpg)

Flop Ratio=1613/14876
Flop Ratio=0.1084


DAY2

Chip Floorplanning

**Die and Core**
Core is the place in which all logical cells are placed. The outer area surrounding the core is called the die. Inbetween the core and the die the I/O pins are placed.

Utilization factor
 - Area occupied by Netlist/Total area of the core.
 - Depending on the UF the extra cells can be added.

Aspect Ratio
 - Ratio of height of the core to the width of the core.
 - If the AR=1 chip shape is square, if AR<1 chip shape is rectangle.

**Preplaced Cells**
They are placed only once in the chip but can be divided into blocks to implement a logic multiple times. Some of them are Memory, Comaparator and Multiplexer.

**Decoupling Capacitors**
They are used to charge the circuit and decouples a circuit from its main voltage source. The loss is reduced as they are physically placed closely to the respective circuits.

**Power Planning**
The power lines are placed vertically and horizontally to avoid voltage drop.

OpenLane Tools for Floorplanning

 - `init_fp` - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing).
 - `ioplacer` - Places the macro input and output ports.
 - `pdn` - Generates the power distribution network.
 - `tapcell` - Inserts welltap and decap cells in the floorplan.

```
run_floorplan
```
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY2/run_floorplan.jpg)

![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY2/Picorv32_floorplan.jpg)

Floorplan def file
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY2/def_floorplan.jpg)


![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY2/magic_command.jpg)

Floorplan in Magic
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY2/magic_floorplan.jpg)

Magic Tcon for Floorplan
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY2/magic_tcon.jpg)


PLACEMENT

OpenLane Tools for Floorplanning

 -   `RePLace`  - Performs global placement.
 -  `Resizer`  - Performs optional optimizations on the design.
 - `OpenDP`  - Perfroms detailed placement to legalize the globally placed components

```
run_placement
```
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY2/placement_command.jpg)

Placement Def file
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY2/def_placement.jpg)

Placement in Magic
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY2/magic_placement.jpg)

**CELL DESIGN FLOW** 

Need for Characterization

"Gates" or "Cells" are the most common parameter across all stage from Logic synthesis to Static timing analysis. So there is a need to charzterize them in a way that all the EDA tools are able to understand them. 

The Cell  Design flow is divided into three stages.

|Inputs| DRC & LVS ckecks, SPICE models, Library and User Defined Specs |
|Design Steps| Circuit design, Layout Design and Chrazterization|
|Output| CDL, GSDII, LEF , Extracted Spice Netlist(.cir), Timing,Noise and     Power Libs function |

The cell design flow is as below

 1. Read the model files.
 2. Read extracted Spice Netlist(.cir).
 3. Recognise the behaviour of the buffer.
 4. Read Sub circuits.
 5. Apply Power supply and the Stimulus.
 6. Provide necessary output capacitcance.
 7. Enter the simulation commands

Feed the above as config file to GUNA to generate the Timing, Power and Noise Libs.

DAY 3

Cloning the file
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY3/cloning_vsd.jpg)

Sky130 tech file
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY3/sky130_tech.jpg)

Sky130 Mag file
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY3/sky130_mag.jpg)

Magic Command to open Layout
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY3/magic_command_vsd.jpg)

Inverter magic layout
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY3/inverter_magic%20.jpg)

Various types of metals in magic
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY3/metals.jpg)

Tkcon file
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY3/tkcon_inverter.jpg)

When we remove a element from layout the DRC tab is changed from 0 
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY3/drc_check.jpg)

Parasitics are extracted in tkcon
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY3/tkcon_spice.jpg)

Sky130_inv_spice File
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY3/invspice_created.jpg)

Spice deck file
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY3/spicedeck%20file.jpg)


```
ngspice sky130_inv.spice
```
Simulation is run in Ngspice
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY3/transient.jpg)

Transient analysis plot
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY3/waveform.jpg)

DAY 4

Horizontal and vertical track info of every metal layer
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/trackinfo.jpg)

Enter the grid information in tkcon
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/tkcongrid.jpg)

The inputs and outputs are present in intersection of the grid.
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/interconnect.jpg)

Define the ports
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/label.jpg)

To Extract the LEF file
![enter image description here](%5Benter%20link%20description%20here%5D%28https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/lef_write.jpg%29)

Inside lef file
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/lef_file.jpg)

SRC directory in runs before lef file 
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/srcbefore%20lef.jpg)

Lef file is copied to SRC directory in Runs
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/lefinsrc.jpg)


Integrate custom cell to our design
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/libfilesinsrc.jpg)

sky130_fd_sc_hd_fast.lib
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/fastlib.jpg)

sky130_fd_sc_hd_slow.lib
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/slowlib.jpg)

sky130_fd_sc_hd_typical.lib
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/typicallib.jpg)

The config.tcl file is modified
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/configtcl.jpg)

```
% prep -design picorv32a -tag 23-09_07-29 -overwrite
```
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/prep.jpg)

```
% set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
% add_lefs -src $lefs
```
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/setlefs.jpg)


```
run_synthesis
run_floorplan
run_placement
```
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/synthesis.jpg)

Our vsdinv inverter is present

![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/vsdinvpresent.jpg)

Slack violation

![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY4/slackviolate.jpg)


STA

OpenLane Tools for STA

 -   `TritonCTS`  - Synthesizes the clock distribution network (the clock tree)


DAY5

**POWER DISTRIBUTION NETWORK**

```
gen_pdn
```
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY5/pdn1.jpg)

![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY5/pdn2.jpg)

## Routing

Routing is the best possible connection between two points, namely source and target. There are various algorithms such as Maze routing, Line searching to perform routing. 

Steps:
 - A routing grid is created with Source and target points defined.
 - Labels the adjacent grids with next integers from source till the target.
 - Find the best possible route from Source to target from multiple available routes.
 - 
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY5/adjacentcells.jpg)

DRC Checks
DRC checks verifies if all the constraints specified are met in the design. There are various types of DRC viloations such as Signal short, Minimun width, Minimun area, Minimum spacing etc that needs to be checked and corrected.

![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY5/drc%20violation.jpg)

OpenLane tools for Routing

 -  `FastRoute`  - Performs global routing to generate a guide file for the detailed router
 -   `CU-GR`  - Another option for performing global routing.
 - `TritonRoute`  - Performs detailed routing.
 - `SPEF-Extractor`  - Performs SPEF extraction

```
run_routing
```
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY5/routing.jpg)

Routing in Magic
![enter image description here](https://github.com/Krishnakumar-Pugazhenthi/Advanced-Physical-Design-using-OpenLANE-SKY130/blob/main/DAY5/magic_routing.jpg)

