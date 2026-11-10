# EXPERIMENT 1

# Minimization and Implementation of Boolean Function

## Aim

To minimize and implement a Boolean function using logic gates and verify the functionality using Synopsys VCS and DVE.

---

## Software Required

- Synopsys VCS
- Synopsys DVE
- Linux Terminal
- Verilog HDL

---

## Boolean Function

Consider the Boolean function:

\[
F(A,B,C,D)=\Sigma m(0,2,5,7,8,10,13,15)
\]

The minimized Boolean expression is:

\[
F = B'D' + BD
\]

The function is implemented using Verilog HDL.

---

## Files Used

| File Name | Description |
|------------|------------|
| `exp1_boolean_min.v` | Verilog design file |
| `exp1_boolean_min_tb.v` | Verilog testbench |
| `exp1_boolean_min.vcd` | VCD waveform dump generated during simulation |

---

## Verilog Design File

```verilog
// gedit fun.v

module fun (
    input wire A,
    input wire B,
    output wire F
);

assign F = (~A) | B;   // F = A' + B

endmodule
```

---

## Verilog Testbench

```verilog
// gedit tb.v

module tb;

    reg A, B;
    wire F;

    // Instantiate the design under test (DUT)
    fun uut (
        .A(A),
        .B(B),
        .F(F)
    );

    initial begin

        // ---- VCD dump setup ----
        $dumpfile("fun.vcd");     // name of the VCD file to be generated
        $dumpvars(0, tb);         // dump all signals in this testbench hierarchy

        // ---- Apply all 4 input combinations ----
        $monitor("Time=%0t A=%b B=%b | F=%b",
                  $time, A, B, F);

        A = 0; B = 0; #10;
        A = 0; B = 1; #10;
        A = 1; B = 0; #10;
        A = 1; B = 1; #10;

        #10 $finish;
    end

endmodule
```

---

## Truth Table
<img width="795" height="311" alt="image" src="https://github.com/user-attachments/assets/dd4ba5b9-016b-4ae5-a693-f309c60c4c0e" />

---

## Simulation Procedure

### STEP 1 – Open Terminal

Open a terminal in the experiment folder.

```bash
cd <experiment_folder>
```

### STEP 2 – Load Synopsys Environment

```bash
source /synopsys/start.sh
```

### STEP 3 – Compile Using VCS

```bash
vcs exp1_boolean_min.v exp1_boolean_min_tb.v -full64
```

If compilation is successful, VCS generates the simulation executable:

```bash
simv
```

### STEP 4 – Run Simulation

```bash
./simv
```

The terminal displays the input combinations and corresponding output **F**.

A VCD waveform file is also generated:

```text
exp1_boolean_min.vcd
```

### STEP 5 – Open DVE

```bash
dve -full64
```

or

```bash
dve -full64 &
```

A DVE environment will open.

---

## DVE Waveform Verification

In DVE:

1. Open the testbench hierarchy.
2. Locate the signals:
   - A
   - B
   - F
3. Add the signals to the waveform window.
4. Run and inspect the waveform.
5. Verify that:
   - F = 1 whenever A = 0 or B = 1.
   - F = 0 only when A = 1 and B = 0.
6. Confirm that the waveform matches the truth table.

---

## Expected Result

The Boolean function was minimized and implemented using Verilog HDL.

The design was successfully compiled and simulated using Synopsys VCS, and the generated waveform was verified using Synopsys DVE.

---

## Output
<img width="1868" height="950" alt="Exp1-output" src="https://github.com/user-attachments/assets/882bd6d7-4259-473f-86fc-8f1100c6422b" />


- Successful compilation of the Verilog program.
- Simulation results displayed in the terminal.
- VCD file generated successfully.
- Waveforms observed and verified in DVE.

---

## Viva-Voce Questions

1. What is Boolean function minimization?
2. What is a minterm?
3. What is a Karnaugh Map (K-Map)?
4. Why is Boolean minimization required?
5. What are universal gates?
6. What is the difference between SOP and POS forms?
7. What is the purpose of a Verilog testbench?
8. Why is a VCD file generated?
9. What is the purpose of `./simv`?
10. What is the purpose of DVE?
11. What is the difference between simulation and synthesis?
12. Why are some variables absent from a minimized expression?
13. What is the purpose of `$dumpfile`?
14. What is the purpose of `$dumpvars`?

---

## Result

Thus, the Boolean function was minimized, implemented using Verilog HDL, successfully simulated using Synopsys VCS, and verified using Synopsys DVE.

