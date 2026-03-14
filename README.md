# 5-Bit Carry Lookahead Adder (CLA) Design & Layout

A complete implementation of a 5-bit Carry Lookahead Adder using TSMC 180nm technology, including circuit simulation and physical layout design.

## Project Overview

This project presents a full-custom design of a 5-bit Carry Lookahead Adder (CLA), a fast arithmetic circuit that reduces propagation delay compared to ripple carry adders. The design includes:

- **Circuit Design & Simulation**: SPICE-based pre-layout and post-layout simulations
- **Physical Layout**: Magic tool-based mask design for TSMC 180nm process
- **Components**: Custom designs for basic logic gates and adder cells

## Project Structure

### Magic Files (Layout Design)
Layout mask designs created using Magic tool for TSMC 180nm technology:

- **CLA.mag / CLA.ext** - 5-bit Carry Lookahead Adder main layout and extracted view
- **and_2.mag / and_2.ext** - 2-input AND gate layout and parasitic extraction
- **xor.mag / xor.ext** - XOR gate layout and parasitic extraction
- **inv.mag / inv.ext** - Inverter/NOT gate layout and parasitic extraction
- **tspc.mag / tspc.ext** - TSPC (True Single Phase Clock) latch design
- **Mcc.mag / Mcc.ext** - Multiplexer/Cross-coupled latch variant

### Technology File
- **SCN6M_DEEP.09.tech27** - 

  - Contains process layers, design rules, and metal stack information
  - Defines layer properties, colors, and accessibility for mask design
  - Required by Magic tool for correct layout representation and DRC (Design Rule Check)
  - Enables accurate parasitic extraction for post-layout simulation

### Ngspice Files (Simulation)
SPICE netlist files for pre-layout and post-layout circuit simulation:

**File Types:**
- **.spice files** - Automatically generated netlists extracted from Magic layout files using `ext2spice` command. These contain the circuit netlist with parasitic RC parameters extracted from the physical layout (post-layout simulation).
- **.cir files** - Manually written NGspice testbench files for circuit testing and functional verification. These contain simulation directives, test vectors, and measurement commands for verification.

#### Extracted Layout Netlists (.spice)
- **CLA.spice** - Main 5-bit CLA SPICE netlist (extracted from CLA.mag)
- **and_2.spice** - 2-input AND gate netlist (extracted from and_2.mag)
- **xor.spice** - XOR gate netlist (extracted from xor.mag)
- **inv.spice** - Inverter gate netlist (extracted from inv.mag)
- **tspc.spice** - TSPC latch netlist (extracted from tspc.mag)
- **Mcc.spice** - Multiplexer cell netlist (extracted from Mcc.mag)

#### Test & Simulation Files (.cir)
- **CLA.cir** - CLA complete circuit testbench with simulation commands
- **gates.cir** - Basic logic gates (AND, XOR, INV) simulation and verification
- **mcc.cir** - Multiplexer cell testing
- **tspcff.cir** - TSPC flip-flop variant testbench

#### Technology & Configuration
- **TSMC_180nm.txt** - TSMC 180nm process technology parameters and models

### Documentation
- **README.md** - This file

## Circuit Design Details

### Carry Lookahead Adder
The CLA improves addition speed by calculating carries in parallel using generate (G) and propagate (P) signals:
- **G = A·B** (carry generate)
- **P = A⊕B** (carry propagate)

### Advantages over Ripple Carry Adder
- Reduced delay: O(log n) vs O(n)
- Higher throughput for multi-bit additions
- Suitable for high-speed arithmetic operations

### Technology Specifications
- **Process**: TSMC 180nm (0.18µm)
- **Supply Voltage**: Standard (typically 1.8V)
- **Temperature Range**: 0°C to 70°C (typical)

## How to Use

### Running Pre-Layout Simulations
1. Use ngspice to run the pre-layout netlists:
   ```bash
   ngspice CLA.spice
   ```

2. Alternatively, use circuit files with testbenches:
   ```bash
   ngspice CLA.cir
   ```

### Viewing & Editing Layouts
1. Open Magic tool and load layout files:
   ```bash
   magic -T SCN6M_DEEP.09.tech27 CLA.mag

   ```

2. To extract parasitic information:
   ```bash
   extract all
   ext2spice
   ```

### Post-Layout Simulation
1. Extract RC parasitic data from layouts using Magic
2. Run simulations with extracted parasitic files (.ext)
3. Compare pre-layout and post-layout results to verify timing

## Design Hierarchy

```
CLA (5-bit Adder)
├── AND gates (and_2)
├── XOR gates (xor)
├── Inverters (inv)
├── TSPC latches (tspc)
└── Multiplexers/Latches (Mcc)
```

## Key Files for Simulation Testing

- **CLA.spice** - Primary simulation netlist
- **gates.cir** - Gate definitions for circuit simulation
- **TSMC_180nm.txt** - Process technology models


## Tools Required

- **Magic** - For layout design and parasitic extraction
- **Ngspice** - For circuit simulation and verification

## Performance Characteristics

The 5-bit CLA offers improved performance over ripple carry adders:
- **Critical Path**: Reduced due to parallel carry computation
- **Area**: Slightly larger than ripple carry (additional logic for carry lookahead)
- **Power**: Comparable to ripple carry for nominal operation

## Future Enhancements

- Extended bit-width implementations (8, 16, 32-bit)
- Variable voltage operation analysis
- Automated layout generation and optimization
- Power consumption analysis
- Timing characterization across PVT corners

## Notes

- All designs follow TSMC 180nm standard cell library conventions
- Extract (.ext) files contain parasitic capacitance and resistance information
- Pre-layout and post-layout simulations should be compared for design closure

## Author & License

Design Project: 5-bit CLA using TSMC 180nm Technology

For questions or contributions, please refer to the project repository.

