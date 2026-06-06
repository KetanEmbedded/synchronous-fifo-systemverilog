# Synchronous FIFO Memory — SystemVerilog

A parameterized synchronous FIFO (First-In-First-Out) memory designed and verified in SystemVerilog.

## Overview

This project implements a synchronous FIFO using a circular buffer architecture. Both write and read operations are governed by the same clock signal. The design is fully parameterized, allowing reuse across different depths and data widths.

## Features

- Parameterized `DEPTH` and `WIDTH` for easy reuse
- Circular buffer with wrap-around write & read pointer logic
- Occupancy counter for real-time status tracking
- Combinational `full` and `empty` flag generation
- Active-low synchronous reset (`rst_n`)
- One-cycle registered read latency

## File Structure

```
├── fifo.sv        # RTL Design
├── fifo_tb.sv     # Testbench
└── README.md
```

## Parameters

| Parameter | Default | Description              |
|-----------|---------|--------------------------|
| `DEPTH`   | 8       | Number of words in FIFO  |
| `WIDTH`   | 8       | Bit-width of each word   |

## Ports

| Port       | Direction | Width     | Description              |
|------------|-----------|-----------|--------------------------|
| `clk`      | Input     | 1         | Clock signal             |
| `rst_n`    | Input     | 1         | Active-low reset         |
| `wr_en`    | Input     | 1         | Write enable             |
| `rd_en`    | Input     | 1         | Read enable              |
| `wr_data`  | Input     | WIDTH     | Data to write            |
| `rd_data`  | Output    | WIDTH     | Data read out            |
| `full`     | Output    | 1         | FIFO full flag           |
| `empty`    | Output    | 1         | FIFO empty flag          |

## Testbench — Test Scenarios

| Test | Description                          | Expected Result              |
|------|--------------------------------------|------------------------------|
| 1    | Fill FIFO with DEPTH words           | `full` flag asserts          |
| 2    | Write to full FIFO (overflow attempt)| Write ignored, no corruption |
| 3    | Read all data out                    | `empty` flag asserts         |
| 4    | Simultaneous read + write            | Count unchanged, no errors   |

## Simulation

Simulated on **EDA Playground** using **Icarus Verilog**.  
Waveforms verified on **EPWave**.

To run on EDA Playground:
1. Paste `fifo.sv` in the design file
2. Paste `fifo_tb.sv` in the testbench file
3. Select **Icarus Verilog** as simulator
4. Enable **Open EPWave** option
5. Click **Run**
