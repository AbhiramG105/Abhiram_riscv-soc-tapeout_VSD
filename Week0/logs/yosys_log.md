# Logs

This folder contains the log outputs of tools that do not have a GUI.
The outputs are generated from simple test cases to verify correct installation.

---

## Yosys

### Code
```bash
echo 'module top(input a, b, output y); assign y = a & b; endmodule' > top.v
yosys -p "read_verilog top.v; synth; stat; show" 
```

### Output
```

 /----------------------------------------------------------------------------\
 |                                                                            |
 |  yosys -- Yosys Open SYnthesis Suite                                       |
 |                                                                            |
 |  Copyright (C) 2012 - 2020  Claire Xenia Wolf <claire@yosyshq.com>         |
 |                                                                            |
 |  Permission to use, copy, modify, and/or distribute this software for any  |
 |  purpose with or without fee is hereby granted, provided that the above    |
 |  copyright notice and this permission notice appear in all copies.         |
 |                                                                            |
 |  THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES  |
 |  WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF          |
 |  MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR   |
 |  ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES    |
 |  WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN     |
 |  ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF   |
 |  OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.            |
 |                                                                            |
 \----------------------------------------------------------------------------/

 Yosys 0.33 (git sha1 2584903a060)


-- Running command `read_verilog top.v; synth; stat; show' --

1. Executing Verilog-2005 frontend: top.v
Parsing Verilog input from `top.v' to AST representation.
Generating RTLIL representation for module `\top'.
Successfully finished Verilog frontend.

2. Executing SYNTH pass.

2.1. Executing HIERARCHY pass (managing design hierarchy).

2.2. Executing PROC pass (convert processes to netlists).

2.2.1. Executing PROC_CLEAN pass (remove empty switches from decision trees).
Cleaned up 0 empty switches.

2.2.2. Executing PROC_RMDEAD pass (remove dead branches from decision trees).
Removed a total of 0 dead cases.

2.2.3. Executing PROC_PRUNE pass (remove redundant assignments in processes).
Removed 0 redundant assignments.
Promoted 0 assignments to connections.

2.2.4. Executing PROC_INIT pass (extract init attributes).

2.2.5. Executing PROC_ARST pass (detect async resets in processes).

2.2.6. Executing PROC_ROM pass (convert switches to ROMs).
Converted 0 switches.

2.2.7. Executing PROC_MUX pass (convert decision trees to multiplexers).

2.2.8. Executing PROC_DLATCH pass (convert process syncs to latches).

2.2.9. Executing PROC_DFF pass (convert process syncs to FFs).

2.2.10. Executing PROC_MEMWR pass (convert process memory writes to cells).

2.2.11. Executing PROC_CLEAN pass (remove empty switches from decision trees).
Cleaned up 0 empty switches.

2.2.12. Executing OPT_EXPR pass (perform const folding).
Optimizing module top.

2.3. Executing OPT_EXPR pass (perform const folding).
Optimizing module top.

2.4. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \top..
Removed 0 unused cells and 1 unused wires.
<suppressed ~1 debug messages>

2.5. Executing CHECK pass (checking for obvious problems).
Checking module top...
Found and reported 0 problems.

2.6. Executing OPT pass (performing simple optimizations).

2.6.1. Executing OPT_EXPR pass (perform const folding).
Optimizing module top.

2.6.2. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\top'.
Removed a total of 0 cells.

2.6.3. Executing OPT_MUXTREE pass (detect dead branches in mux trees).
Running muxtree optimizer on module \top..
  Creating internal representation of mux trees.
  No muxes found in this module.
Removed 0 multiplexer ports.

2.6.4. Executing OPT_REDUCE pass (consolidate $*mux and $reduce_* inputs).
  Optimizing cells in module \top.
Performed a total of 0 changes.

2.6.5. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\top'.
Removed a total of 0 cells.

2.6.6. Executing OPT_DFF pass (perform DFF optimizations).

2.6.7. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \top..

2.6.8. Executing OPT_EXPR pass (perform const folding).
Optimizing module top.

2.6.9. Finished OPT passes. (There is nothing left to do.)

2.7. Executing FSM pass (extract and optimize FSM).

2.7.1. Executing FSM_DETECT pass (finding FSMs in design).

2.7.2. Executing FSM_EXTRACT pass (extracting FSM from design).

2.7.3. Executing FSM_OPT pass (simple optimizations of FSMs).

2.7.4. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \top..

2.7.5. Executing FSM_OPT pass (simple optimizations of FSMs).

2.7.6. Executing FSM_RECODE pass (re-assigning FSM state encoding).

2.7.7. Executing FSM_INFO pass (dumping all available information on FSM cells).

2.7.8. Executing FSM_MAP pass (mapping FSMs to basic logic).

2.8. Executing OPT pass (performing simple optimizations).

2.8.1. Executing OPT_EXPR pass (perform const folding).
Optimizing module top.

2.8.2. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\top'.
Removed a total of 0 cells.

2.8.3. Executing OPT_MUXTREE pass (detect dead branches in mux trees).
Running muxtree optimizer on module \top..
  Creating internal representation of mux trees.
  No muxes found in this module.
Removed 0 multiplexer ports.

2.8.4. Executing OPT_REDUCE pass (consolidate $*mux and $reduce_* inputs).
  Optimizing cells in module \top.
Performed a total of 0 changes.

2.8.5. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\top'.
Removed a total of 0 cells.

2.8.6. Executing OPT_DFF pass (perform DFF optimizations).

2.8.7. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \top..

2.8.8. Executing OPT_EXPR pass (perform const folding).
Optimizing module top.

2.8.9. Finished OPT passes. (There is nothing left to do.)

2.9. Executing WREDUCE pass (reducing word size of cells).

2.10. Executing PEEPOPT pass (run peephole optimizers).

2.11. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \top..

2.12. Executing ALUMACC pass (create $alu and $macc cells).
Extracting $alu and $macc cells in module top:
  created 0 $alu and 0 $macc cells.

2.13. Executing SHARE pass (SAT-based resource sharing).

2.14. Executing OPT pass (performing simple optimizations).

2.14.1. Executing OPT_EXPR pass (perform const folding).
Optimizing module top.

2.14.2. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\top'.
Removed a total of 0 cells.

2.14.3. Executing OPT_MUXTREE pass (detect dead branches in mux trees).
Running muxtree optimizer on module \top..
  Creating internal representation of mux trees.
  No muxes found in this module.
Removed 0 multiplexer ports.

2.14.4. Executing OPT_REDUCE pass (consolidate $*mux and $reduce_* inputs).
  Optimizing cells in module \top.
Performed a total of 0 changes.

2.14.5. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\top'.
Removed a total of 0 cells.

2.14.6. Executing OPT_DFF pass (perform DFF optimizations).

2.14.7. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \top..

2.14.8. Executing OPT_EXPR pass (perform const folding).
Optimizing module top.

2.14.9. Finished OPT passes. (There is nothing left to do.)

2.15. Executing MEMORY pass.

2.15.1. Executing OPT_MEM pass (optimize memories).
Performed a total of 0 transformations.

2.15.2. Executing OPT_MEM_PRIORITY pass (removing unnecessary memory write priority relations).
Performed a total of 0 transformations.

2.15.3. Executing OPT_MEM_FEEDBACK pass (finding memory read-to-write feedback paths).

2.15.4. Executing MEMORY_BMUX2ROM pass (converting muxes to ROMs).

2.15.5. Executing MEMORY_DFF pass (merging $dff cells to $memrd).

2.15.6. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \top..

2.15.7. Executing MEMORY_SHARE pass (consolidating $memrd/$memwr cells).

2.15.8. Executing OPT_MEM_WIDEN pass (optimize memories where all ports are wide).
Performed a total of 0 transformations.

2.15.9. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \top..

2.15.10. Executing MEMORY_COLLECT pass (generating $mem cells).

2.16. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \top..

2.17. Executing OPT pass (performing simple optimizations).

2.17.1. Executing OPT_EXPR pass (perform const folding).
Optimizing module top.

2.17.2. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\top'.
Removed a total of 0 cells.

2.17.3. Executing OPT_DFF pass (perform DFF optimizations).

2.17.4. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \top..

2.17.5. Finished fast OPT passes.

2.18. Executing MEMORY_MAP pass (converting memories to logic and flip-flops).

2.19. Executing OPT pass (performing simple optimizations).

2.19.1. Executing OPT_EXPR pass (perform const folding).
Optimizing module top.

2.19.2. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\top'.
Removed a total of 0 cells.

2.19.3. Executing OPT_MUXTREE pass (detect dead branches in mux trees).
Running muxtree optimizer on module \top..
  Creating internal representation of mux trees.
  No muxes found in this module.
Removed 0 multiplexer ports.

2.19.4. Executing OPT_REDUCE pass (consolidate $*mux and $reduce_* inputs).
  Optimizing cells in module \top.
Performed a total of 0 changes.

2.19.5. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\top'.
Removed a total of 0 cells.

2.19.6. Executing OPT_SHARE pass.

2.19.7. Executing OPT_DFF pass (perform DFF optimizations).

2.19.8. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \top..

2.19.9. Executing OPT_EXPR pass (perform const folding).
Optimizing module top.

2.19.10. Finished OPT passes. (There is nothing left to do.)

2.20. Executing TECHMAP pass (map to technology primitives).

2.20.1. Executing Verilog-2005 frontend: /usr/bin/../share/yosys/techmap.v
Parsing Verilog input from `/usr/bin/../share/yosys/techmap.v' to AST representation.
Generating RTLIL representation for module `\_90_simplemap_bool_ops'.
Generating RTLIL representation for module `\_90_simplemap_reduce_ops'.
Generating RTLIL representation for module `\_90_simplemap_logic_ops'.
Generating RTLIL representation for module `\_90_simplemap_compare_ops'.
Generating RTLIL representation for module `\_90_simplemap_various'.
Generating RTLIL representation for module `\_90_simplemap_registers'.
Generating RTLIL representation for module `\_90_shift_ops_shr_shl_sshl_sshr'.
Generating RTLIL representation for module `\_90_shift_shiftx'.
Generating RTLIL representation for module `\_90_fa'.
Generating RTLIL representation for module `\_90_lcu'.
Generating RTLIL representation for module `\_90_alu'.
Generating RTLIL representation for module `\_90_macc'.
Generating RTLIL representation for module `\_90_alumacc'.
Generating RTLIL representation for module `\$__div_mod_u'.
Generating RTLIL representation for module `\$__div_mod_trunc'.
Generating RTLIL representation for module `\_90_div'.
Generating RTLIL representation for module `\_90_mod'.
Generating RTLIL representation for module `\$__div_mod_floor'.
Generating RTLIL representation for module `\_90_divfloor'.
Generating RTLIL representation for module `\_90_modfloor'.
Generating RTLIL representation for module `\_90_pow'.
Generating RTLIL representation for module `\_90_pmux'.
Generating RTLIL representation for module `\_90_demux'.
Generating RTLIL representation for module `\_90_lut'.
Successfully finished Verilog frontend.

2.20.2. Continuing TECHMAP pass.
Using extmapper simplemap for cells of type $and.
No more expansions possible.
<suppressed ~74 debug messages>

2.21. Executing OPT pass (performing simple optimizations).

2.21.1. Executing OPT_EXPR pass (perform const folding).
Optimizing module top.

2.21.2. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\top'.
Removed a total of 0 cells.

2.21.3. Executing OPT_DFF pass (perform DFF optimizations).

2.21.4. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \top..

2.21.5. Finished fast OPT passes.

2.22. Executing ABC pass (technology mapping using ABC).

2.22.1. Extracting gate netlist of module `\top' to `<abc-temp-dir>/input.blif'..
Extracted 1 gates and 3 wires to a netlist network with 2 inputs and 1 outputs.

2.22.1.1. Executing ABC.
Running ABC command: "<yosys-exe-dir>/yosys-abc" -s -f <abc-temp-dir>/abc.script 2>&1
ABC: ABC command line: "source <abc-temp-dir>/abc.script".
ABC:
ABC: + read_blif <abc-temp-dir>/input.blif
ABC: + read_library <abc-temp-dir>/stdcells.genlib
ABC: Entered genlib library with 13 gates from file "<abc-temp-dir>/stdcells.genlib".
ABC: + strash
ABC: + dretime
ABC: + map
ABC: + write_blif <abc-temp-dir>/output.blif

2.22.1.2. Re-integrating ABC results.
ABC RESULTS:               AND cells:        1
ABC RESULTS:        internal signals:        0
ABC RESULTS:           input signals:        2
ABC RESULTS:          output signals:        1
Removing temp directory.

2.23. Executing OPT pass (performing simple optimizations).

2.23.1. Executing OPT_EXPR pass (perform const folding).
Optimizing module top.

2.23.2. Executing OPT_MERGE pass (detect identical cells).
Finding identical cells in module `\top'.
Removed a total of 0 cells.

2.23.3. Executing OPT_DFF pass (perform DFF optimizations).

2.23.4. Executing OPT_CLEAN pass (remove unused cells and wires).
Finding unused cells or wires in module \top..
Removed 0 unused cells and 3 unused wires.
<suppressed ~1 debug messages>

2.23.5. Finished fast OPT passes.

2.24. Executing HIERARCHY pass (managing design hierarchy).

2.25. Printing statistics.

=== top ===

   Number of wires:                  3
   Number of wire bits:              3
   Number of public wires:           3
   Number of public wire bits:       3
   Number of memories:               0
   Number of memory bits:            0
   Number of processes:              0
   Number of cells:                  1
     $_AND_                          1

2.26. Executing CHECK pass (checking for obvious problems).
Checking module top...
Found and reported 0 problems.

3. Printing statistics.

=== top ===

   Number of wires:                  3
   Number of wire bits:              3
   Number of public wires:           3
   Number of public wire bits:       3
   Number of memories:               0
   Number of memory bits:            0
   Number of processes:              0
   Number of cells:                  1
     $_AND_                          1
```
