# DualVth assignment

Development of a TCL script, to be run by the Synopsys PrimeTime analysis tool.  
The code is expected to operate on an already synthesized combinational circuit, in order to reduce the leakage power dissipation, while keeping the slack as high as possible.  
The optimization is achieved by substituting some cells with other cells that have the same purpose, but operate with a higher threshold voltage. This reduces the leakage current but also decreases the speed of the cell, and consequently alters the slack of its path.

The script adopts a logarithmic technique trading off between efficiency and execution time.  
The *__Report.pdf__* better exlplains the glocal flow of the algorithm, adn the reasons behind it.

Project developed for the course of Synthesis and Optimization of Digital Systems at Politecnico di Torino, year 2016-2017.

## Running the script

Before being able to run the DualVth assignment script, the design must be synthesized by DesignCompiler and analyzed by PrimeTime.  
While not sufficient to reproduce the whole process, the *synthesis.tcl* and *pt_analysis.tcl* scripts are provided to understand the synthesis flow.  

Then, the DualVth script can be executed. It accepts two arguments:  
+ lvt: the maximum percentage of LVT (Low Voltage Threshold) cells that can be left in the circuit at the end of the elaboration  
+ constraint: *hard* or *soft*. When the constraint is hard, the *lvt* argument must be respected even if it means obtaining a negative slack: this means that reducing the leakage power is more important than timing constraints. When the constraint is soft, the slack must not go under 0, even if it means not fulfilling the *lvt* agrument.

Usage examples:

```

>We want to swap at least 60% of the cells, even if the slack becomes negative
dualVth -lvt 0.4 -constraint hard

>We would like to swap 20% of the cells, or get as close as possible with a positive slack
dualVth -lvt 0.8 -constraint soft

>We want to swap as many cells as possible, while keeping a positive slack
dualVth -lvt 0 -constraint soft

```
