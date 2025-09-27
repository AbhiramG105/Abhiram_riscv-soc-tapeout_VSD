# Logs

This folder contains the log outputs of tools.                                                  
The outputs are generated from simple test cases to verify correct installation.

---

## Icarus Verilog

### Code
```bash
echo 'module m; initial $display("iverilog_ok"); endmodule' > t.v
iverilog t.v -o t.out && ./t.out
```

### Output
```
iverilog_ok
```
