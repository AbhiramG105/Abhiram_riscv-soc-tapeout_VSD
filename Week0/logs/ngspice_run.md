# Logs

This folder contains the log outputs of tools.                                                  
The outputs are generated from simple test cases to verify correct installation.

---

## NGSpice

### Code
```bash
 # Create a basic RC circuit netlist
echo '* RC low-pass filter example
V1 in 0 PULSE(0 5 0 0.1m 0.1m 1m 2m)
R1 in out 1k
C1 out 0 1u
.tran 0.1m 5m
.control
run
plot v(out)
.endc
.end' > rc_circuit.sp

# Run in ngspice
ngspice rc_circuit.sp
```

### Output
```
******
** ngspice-42 : Circuit level simulation program
** Compiled with KLU Direct Linear Solver
** The U. C. Berkeley CAD Group
** Copyright 1985-1994, Regents of the University of California.
** Copyright 2001-2023, The ngspice team.
** Please get your ngspice manual from https://ngspice.sourceforge.io/docs.html
** Please file your bug-reports at http://ngspice.sourceforge.net/bugrep.html
** Creation Date: Sun Mar 31 20:15:14 UTC 2024
******

Note: No compatibility mode selected!


Circuit: * rc low-pass filter example

Doing analysis at TEMP = 27.000000 and TNOM = 27.000000

Using SPARSE 1.3 as Direct Linear Solver

Initial Transient Solution
--------------------------

Node                                   Voltage
----                                   -------
in                                           0
out                                          0
v1#branch                                    0


No. of Data Rows : 90
```
