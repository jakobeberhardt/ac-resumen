
<!-- TOC start (generated with https://github.com/derlin/bitdowntoc) -->

- [Tema 1 : Fundamentos de diseño y evaluación de computadores](#tema-1--fundamentos-de-diseño-y-evaluación-de-computadores)
  - [Formulas](#formulas)
  - [Texec](#texec)
  - [CPI](#cpi)
    - [Speedup Formula](#speedup-formula)
    - [Needed processors for speedup](#needed-processors-for-speedup)
    - [MIPS (Million Instructions Per Second) Formula](#mips-million-instructions-per-second-formula)
    - [MFLOPS (Million Floating-Point Operations Per Second) Formula](#mflops-million-floating-point-operations-per-second-formula)
- [Tema 2: Interfaz Alto Nivel – Ensamblador](#tema-2-interfaz-alto-nivel--ensamblador)
  - [Computer Architecture Concepts](#computer-architecture-concepts)
    - [EIP (Instruction Pointer)](#eip-instruction-pointer)
    - [Registers](#registers)
    - [Condition Codes](#condition-codes)
    - [Memory](#memory)
  - [Available Registers](#available-registers)
  - [Available Basic Data types](#available-basic-data-types)
  - [Ranges](#ranges)
  - [Addressing Modes](#addressing-modes)
    - [Immediate](#immediate)
    - [Register](#register)
    - [Memory](#memory-1)
  - [Moving Modes](#moving-modes)
  - [Examples of Addressing](#examples-of-addressing)
  - [Sign Extension: `movsbw` Example](#sign-extension-movsbw-example)
  - [Instrucciones Aritmeticas](#instrucciones-aritmeticas)
  - [Logical Operations](#logical-operations)
  - [Sequencing Instructions (Instrucciones de Secuenciamiento)](#sequencing-instructions-instrucciones-de-secuenciamiento)
  - [Example: `je` (Jump if Equal)](#example-je-jump-if-equal)
  - [Flags in Assembly Language](#flags-in-assembly-language)
    - [Zero Flag (ZF)](#zero-flag-zf)
    - [Carry Flag (CF)](#carry-flag-cf)
    - [Sign Flag (SF)](#sign-flag-sf)
    - [Overflow Flag (OF)](#overflow-flag-of)
  - [Data Structures and how to access them](#data-structures-and-how-to-access-them)
  - [Vectors](#vectors)
    - [Long example of accessing a vector element](#long-example-of-accessing-a-vector-element)
  - [Matrix](#matrix)
    - [Long example of accessing a matrix element](#long-example-of-accessing-a-matrix-element)
  - [3D Matrix](#3d-matrix)
  - [Translation Examples](#translation-examples)
    - [Initialize data and run sum over matrix (Estudio Previo L3/1)](#initialize-data-and-run-sum-over-matrix-estudio-previo-l31)
    - [Running sum of matrix sequentially (Estudio Previo L3/2)](#running-sum-of-matrix-sequentially-estudio-previo-l32)
  - [Example of working with multiple data sources](#example-of-working-with-multiple-data-sources)
  - [Data Alignment (32-bit)](#data-alignment-32-bit)
    - [Structs](#structs)
    - [Example of working with structs](#example-of-working-with-structs)
    - [GCC IA32 data type lengths](#gcc-ia32-data-type-lengths)
    - [Addressing fields of the struct](#addressing-fields-of-the-struct)
    - [Addressing fields of the struct in assembly](#addressing-fields-of-the-struct-in-assembly)
  - [Example Lab3 Task 1](#example-lab3-task-1)
    - [Setting up the Stackframe](#setting-up-the-stackframe)
    - [Regeisters that have to be stashed by the subroutine](#regeisters-that-have-to-be-stashed-by-the-subroutine)
    - [Implementation of OperaVec](#implementation-of-operavec)
    - [Optimized Implementation of OperaVec](#optimized-implementation-of-operavec)
  - [TODO: Insert L3 Task 2 (Matrix)](#todo-insert-l3-task-2-matrix)
  - [Example of an Activation Block](#example-of-an-activation-block)
- [Tema 3: Jerarquía de Memorias](#tema-3-jerarquía-de-memorias)
  - [Temporal Locality](#temporal-locality)
  - [Spatial Locality](#spatial-locality)
  - [Cache Memory](#cache-memory)
  - [Placement Algorithms](#placement-algorithms)
    - [Direct Mapping](#direct-mapping)
    - [Set-Associative](#set-associative)
    - [Fully Associative](#fully-associative)
  - [Examples of Placements](#examples-of-placements)
    - [1. Direct Mapping (`Emplazamiento DIRECTO`)](#1-direct-mapping-emplazamiento-directo)
    - [2. Set Associative Mapping (`Emplazamiento ASOCIATIVO por CONJUNTOS`)](#2-set-associative-mapping-emplazamiento-asociativo-por-conjuntos)
    - [3. Fully Associative Mapping (`Emplazamiento COMPLETAMENTE ASOCIATIVO`)](#3-fully-associative-mapping-emplazamiento-completamente-asociativo)
    - [Vorlesung KIT](#vorlesung-kit)
  - [Some cache formulas](#some-cache-formulas)
    - [Average Memory Access Time for Instruction Accesses](#average-memory-access-time-for-instruction-accesses)
    - [Average Memory Access Time for Data Accesses](#average-memory-access-time-for-data-accesses)
    - [Average Memory Access Time for All Accesses](#average-memory-access-time-for-all-accesses)
    - [Time per instruction](#time-per-instruction)
    - [Total CPI](#total-cpi)
    - [Number of Cache Sets and Rows per Set](#number-of-cache-sets-and-rows-per-set)
    - [Blocks per Way:](#blocks-per-way)
    - [Byte Offset](#byte-offset)
    - [Set Index Offset](#set-index-offset)
    - [Set Mapping of Blocks](#set-mapping-of-blocks)
    - [Size in bits of the data memory and the tag memory of one way](#size-in-bits-of-the-data-memory-and-the-tag-memory-of-one-way)
      - [Data memory size:](#data-memory-size)
      - [Tag memory size:](#tag-memory-size)
    - [Average Dynamic Power (!!!):](#average-dynamic-power-)
    - [Average Static Power (!!!):](#average-static-power-)
    - [Average Total Power (!!!):](#average-total-power-)
    - [Power of a CPU-Cache system](#power-of-a-cpu-cache-system)
    - [Energy Consumption](#energy-consumption)
    - [Concepts and considerations](#concepts-and-considerations)
      - [LRU (Least Recently Used)](#lru-least-recently-used)
      - [Copy Back + Write Allocate](#copy-back--write-allocate)
    - [Memory Access](#memory-access)
  - [Virtual Memory: Overview and Performance](#virtual-memory-overview-and-performance)
    - [Why?](#why)
    - [How Configurations Affect Performance](#how-configurations-affect-performance)
    - [Important Formulas and Examples](#important-formulas-and-examples)
      - [Virtual Page Number (VPN) to Physical Page Number (PPN) Translation](#virtual-page-number-vpn-to-physical-page-number-ppn-translation)
      - [Address Translation with TLB](#address-translation-with-tlb)
  - [Conceptos Avanzados de Memoria Cache](#conceptos-avanzados-de-memoria-cache)
  - [1-13](#1-13)
  - [Miss categories](#miss-categories)
  - [Metrics and how to improve them](#metrics-and-how-to-improve-them)
    - [Execution Time Optimization](#execution-time-optimization)
    - [Memory Hierarchy Influence](#memory-hierarchy-influence)
    - [Advanced Memory Hierarchy Concepts: Cache Memory](#advanced-memory-hierarchy-concepts-cache-memory)
      - [Techniques to Improve Cache Performance](#techniques-to-improve-cache-performance)
      - [Advanced Techniques for Cache Performance Enhancement](#advanced-techniques-for-cache-performance-enhancement)
  - [Way Prediction in Cache Memory](#way-prediction-in-cache-memory)
    - [Set-Associative Cache](#set-associative-cache)
    - [Way Prediction Mechanics](#way-prediction-mechanics)
    - [Advantages](#advantages)
    - [Cache Types with Way Prediction](#cache-types-with-way-prediction)
    - [TODO: 050 Cache avanzada](#todo-050-cache-avanzada)
  - [RAM](#ram)
    - [Addresses](#addresses)
    - [Read Access](#read-access)
      - [Row (Fila) via wordline](#row-fila-via-wordline)
      - [Column via bit line](#column-via-bit-line)
    - [Write Access](#write-access)
    - [Process Synchronization Chronogram for DRAM](#process-synchronization-chronogram-for-dram)
    - [Timings](#timings)
    - [Access protocols and "column caching"](#access-protocols-and-column-caching)
    - [Asynchronous Memory](#asynchronous-memory)
    - [Synchronous Memory](#synchronous-memory)
    - [Reusing the @FIL](#reusing-the-fil)
    - [Reusing the @COL](#reusing-the-col)
    - [Summary of the optimizations](#summary-of-the-optimizations)
    - [Lookups](#lookups)
      - [`Same bank, same page`](#same-bank-same-page)
      - [Same page, different bank](#same-page-different-bank)
      - [Same bank, different page](#same-bank-different-page)
    - [RAM Formulas](#ram-formulas)
    - [Cycle time](#cycle-time)
    - [Theoretical Bandwith](#theoretical-bandwith)
    - [Wattage](#wattage)
    - [Energy](#energy)
    - [Memory MTTF (Mbit) (per hour)](#memory-mttf-mbit-per-hour)
    - [MTTF Mbit to bit](#mttf-mbit-to-bit)
  - [Storage](#storage)
    - [Calculating secotor transfer time](#calculating-secotor-transfer-time)
    - [Bandwith of](#bandwith-of)
    - [Effective Bandwith](#effective-bandwith)
    - [RAID](#raid)
    - [RAID Quick Summary](#raid-quick-summary)
      - [RAID 0](#raid-0)
      - [RAID 1](#raid-1)
      - [RAID 2](#raid-2)
      - [RAID 3](#raid-3)
      - [RAID 4](#raid-4)
      - [RAID 5](#raid-5)
        - [Bandwith for sequential read](#bandwith-for-sequential-read)
        - [Bandwith for sequential writes](#bandwith-for-sequential-writes)
        - [Bandwith for random writes](#bandwith-for-random-writes)
      - [RAID 6](#raid-6)
    - [General Observations](#general-observations)
    - [Reliability of different RAID configurations](#reliability-of-different-raid-configurations)
    - [RAID 0](#raid-0-1)
    - [RAID 1 (N = 2)](#raid-1-n--2)
    - [RAID 5](#raid-5-1)
    - [RAID 6](#raid-6-1)
    - [Overview](#overview)
    - [RAID Combinations](#raid-combinations)
    - [RAID 01](#raid-01)
    - [RAID 10](#raid-10)
    - [RAID 51](#raid-51)
    - [RAID 15](#raid-15)
    - [RAID 50](#raid-50)
    - [RAID 05](#raid-05)
  - [Instructions](#instructions)
    - [Stack-Based Architecture](#stack-based-architecture)
      - [Example](#example)
    - [Accumulator-Based Architecture](#accumulator-based-architecture)
      - [Example](#example-1)
    - [Addressing Mode](#addressing-mode)
      - [Definition](#definition)
      - [Components](#components)
      - [Design Criteria](#design-criteria)
    - [Addressing Modes](#addressing-modes-1)
    - [Register Mode](#register-mode)
    - [Immediate Mode](#immediate-mode)
    - [Absolute (Direct) Mode](#absolute-direct-mode)
    - [Register Indirect Mode](#register-indirect-mode)
    - [Base + Displacement Mode](#base--displacement-mode)
    - [Indexed Mode](#indexed-mode)
    - [Scaled Mode](#scaled-mode)
    - [Post-Indirection](#post-indirection)
    - [Post-Scaling](#post-scaling)
    - [CISC: Complex Instruction Set Computer](#cisc-complex-instruction-set-computer)
    - [RISC: Reduced (complexity) Instruction Set Computer](#risc-reduced-complexity-instruction-set-computer)
    - [Objective](#objective)
    - [CISC vs RISC Comparison](#cisc-vs-risc-comparison)
  - [CISC (Complex Instruction Set Computer)](#cisc-complex-instruction-set-computer-1)
  - [RISC (Reduced Instruction Set Computer)](#risc-reduced-instruction-set-computer)
    - [Microprogramming](#microprogramming)
      - [Overview](#overview-1)
      - [Basic Elements of a Processor](#basic-elements-of-a-processor)
      - [Types of Control Units](#types-of-control-units)
    - [Formulas](#formulas-1)
    - [Total Power Consumption](#total-power-consumption)
    - [Energy Consumption](#energy-consumption-1)
    - [Microprogramming](#microprogramming-1)
    - [Example Microprogram of MS](#example-microprogram-of-ms)
    - [Wired Control Unit vs Microprogrammed Control Unit](#wired-control-unit-vs-microprogrammed-control-unit)
      - [Wired Control Unit](#wired-control-unit)
      - [Microprogrammed Control Unit](#microprogrammed-control-unit)
      - [Example](#example-2)
      - [Cost Comparison](#cost-comparison)
        - [Wired Control Unit](#wired-control-unit-1)
        - [Microprogrammed Control Unit](#microprogrammed-control-unit-1)
    - [Assembly Code Examples](#assembly-code-examples)
    - [Compilation vs Interpretation](#compilation-vs-interpretation)
  - [Advanced topics](#advanced-topics)
    - [Basic Techniques in Processor Design](#basic-techniques-in-processor-design)
      - [Memorization](#memorization)
      - [Concurrency](#concurrency)
    - [Summary of Pipeline Processing in CPUs](#summary-of-pipeline-processing-in-cpus)
      - [Overview](#overview-2)
      - [Pipeline Stages](#pipeline-stages)
      - [Pipeline Execution](#pipeline-execution)
      - [Hazards in Pipeline](#hazards-in-pipeline)
      - [Example](#example-3)
      - [Data](#data)
    - [Not All Instructions Have the Same Stages](#not-all-instructions-have-the-same-stages)
      - [Instructions with Variable Execution Time](#instructions-with-variable-execution-time)
      - [Management of Interruptions and Exceptions](#management-of-interruptions-and-exceptions)
    - [SuperScalar Processors](#superscalar-processors)
      - [Goal: CPI \< 1](#goal-cpi--1)
    - [Out-of-Order SuperScalar Processors](#out-of-order-superscalar-processors)
      - [Goal: CPI \< 1](#goal-cpi--1-1)
    - [Example of Out-of-Order Execution in SuperScalar Processors](#example-of-out-of-order-execution-in-superscalar-processors)
      - [Execution Scenario in OoO Processor:](#execution-scenario-in-ooo-processor)
      - [Summary OoO:](#summary-ooo)
    - [VLIW (Very Long Instruction Word)](#vliw-very-long-instruction-word)
      - [Overview](#overview-3)
      - [Characteristics](#characteristics)
      - [Processor Design](#processor-design)
      - [Example of VLIW Architecture](#example-of-vliw-architecture)
      - [Consideration](#consideration)
    - [Overview](#overview-4)
    - [Other formulas](#other-formulas)
      - [Normalizing](#normalizing)
- [Vocabulary](#vocabulary)

<!-- TOC end -->


<!-- TOC --><a name="tema-1-fundamentos-de-diseño-y-evaluación-de-computadores"></a>
# Tema 1 : Fundamentos de diseño y evaluación de computadores
## Formulas

MTTF = Mean time to failure

Error rate (tasa de fallos) = l = 1 / MTTF

MTTR = Mean time to Repair

Availability (Disponibilidad) = MTTF / MTTF + MTTR

Time between errors (tiempo entre errors) = p = 1 - e^-lt

* p = possibility of an error
* l = 1 / MTTF
* t = time

MTTFsystema = 1 / MTTFa + 1 / MTTFb

1 / Performance (Redimiento) = N * CPI * Tcycle
1 / Performance (Redimiento) = time / program = instructions / program * cycles / instruction * time / cycle

Speedup (Ganancia) = Ta / Tb
with

* 1 ⇒ B es más rápido que A
* <1 ⇒ B es más lento que A

## Texec
$$
T = \frac{Cycles}{GHz * 10^9}
$$

## CPI
$$
CPI = \frac{Cycles}{Instructions}
$$

### Speedup Formula
$$
\text{Speedup} = \frac{T_{\text{old}}}{T_{\text{new}}}
$$

### Needed processors for speedup
$$
\text{Processors N for speedup of 5} = P_{\text{sequential}} + \frac{P_{\text{Parallel}}}{N}
$$

### MIPS (Million Instructions Per Second) Formula
$$
\text{MIPS} = \frac{I}{T \times 10^6}
$$

Where:
- \( T \) : Total execution time in seconds
- \( I \) : Total number of instructions executed

### MFLOPS (Million Floating-Point Operations Per Second) Formula
$$
\text{MFLOPS} = \frac{F}{T \times 10^6}
$$

Where:
- \( F \) : Total number of floating-point operations executed
- \( T \) : Total execution time in seconds







# Tema 2: Interfaz Alto Nivel – Ensamblador


## Computer Architecture Concepts

### EIP (Instruction Pointer)

- Points to the next instruction to be executed.

### Registers

- Often used as fast access variables.

### Condition Codes

- Store information regarding the behavior of the last executed instructions.
- Used in conditional jumps.

### Memory

- Addressable vector at byte level.
- Stack for supporting subroutine management.

## Available Registers

![Available Registers](./figures/registros-disponible.png)

## Available Basic Data types

| Data Size | Length in Bits | Representing |
|-----------|----------------|--------------|
| Byte | 8 bits | Integer |
| Word | 16 bits | Integer |
| Longword | 32 bits | Integer |
| Quadword | 64 bits | Floating Point |

## Ranges

| Data Type | Rango Naturales | Rango Enteros |
|-----------|-----------------|---------------|
| byte | 0 ≤ x ≤ 255 | \-128 ≤ x ≤ 127 |
| word | 0 ≤ x ≤ 65,535 | \-32,768 ≤ x ≤ 32,767 |
| longword | 0 ≤ x ≤ 4,294,967,215 | \-2,147,483,648 ≤ x ≤ 2,147,483,647 |

## Addressing Modes

### Immediate

- `$19`
- `$-3`
- `$0x2A`
- `$0x2A45`

*Encoded with 1, 2, or 4 bytes*

### Register

- `%eax`
- `%ah`
- `%esi`

### Memory

- `D(Rb, Ri, s) → M[Rb+Ri×s+D]`

*D: Displacement encoded with 1, 2, or 4 bytes*  
*Rb: Base register. Any of the 8 registers*  
*Ri: Index register. Any except* `%esp`  
*S: Scale factor: 1, 2, 4, or 8*

- **Rb**: This is the base register. It holds the base address of structures like an array or matrix.
- **Ri**: This is the index register. When its value is multiplied by the scale factor `s`, it helps in indexing structures or arrays.
- **s**: This represents the scale factor. For instance, if you're accessing an array of 4-byte integers, `s` would typically be `4`.
- **D**: Known as the displacement, this is an additional offset added to the address calculation.

Given the formula `M[Rb + Ri * s + D]`, it translates to:
"Access the memory at the address calculated by adding the base register's value to the product of the index register's value and the scale factor, then add the displacement. Retrieve (or set) the value at that computed address."

![Effective address](./figures/direccrion-efectiva.png)

## Moving Modes

| Instruction Template | x Values | Verbal | Description |
|----------------------|----------|--------|-------------|
| `movx op1, op2` | L, W, B | Move `op1` to `op2` | Copy value from `op1` to `op2`. The size of the operation is determined by x. |
| `movb $-1,%al` | B (Byte) | Move byte `-1` to `%al` | Places the byte value `-1` into the `%al` register. |
| `movsxy op1, op2` | BW, BL, WL | Sign-extend `op1` and move to `op2` | Takes the value in `op1`, sign-extends it, and places the result in `op2`. |
| `movsbw %ch,%ax` | BW (Byte to Word) | Sign-extend byte `%ch` to word `%ax` | Sign-extends the byte in `%ch` and stores the resulting word in `%ax`. |
| `movzxy op1, op2` | BW, BL, WL | Zero-extend `op1` and move to `op2` | Takes the value in `op1`, zero-extends it, and places the result in `op2`. |
| `movzwl %bx,%edx` | WL (Word to Long) | Zero-extend word `%bx` to long `%edx` | Zero-extends the word in `%bx` and stores the resulting long in `%edx`. |
| `pushl op1` | L (Long) | Push `op1` onto the stack | Decreases `%esp` by 4 and places the long value from `op1` onto the top of the stack. |
| `pushl 12(%ebp)` | L (Long) | Push value at memory location `12(%ebp)` onto the stack | Pushes the value found 12 bytes ahead of `%ebp` onto the stack. |
| `popl op1` | L (Long) | Pop top of stack into `op1` | Takes the long value from the top of the stack and places it into `op1`, then increases `%esp` by 4. |
| `popl %eax` | L (Long) | Pop top of stack into `%eax` | Takes the long value from the top of the stack and places it into `%eax`. |
| `leal op1, op2` | L (Long) | Load address of `op1` into `op2` | Computes the address of `op1` and stores the resulting address in `op2`. |
| `leal (%ebx,%ecx),%eax` | L (Long) | Load address `(%ebx + %ecx)` into `%eax` | Computes the sum of `%ebx` and `%ecx` and places the resulting address in `%eax`. |

## Examples of Addressing

| Addressing Mode | Memory Calculation | Explanation |
|-----------------|--------------------|-------------|
| `(%eax,%ebx)` | `M[eax+ebx]` | Access memory at address resulting from `eax + ebx`. |
| `-3(%eax,%ebx)` | `M[eax+ebx-3]` | Access memory at address resulting from `eax + ebx`, and then subtracting 3. |
| `(,%ebx,4)` | `M[ebx·4]` | Access memory at address resulting from `ebx` multiplied by 4. |
| `(%eax,%ebx,4)` | `M[eax+ebx·4]` | Access memory at address resulting from `eax + (ebx * 4)`. |
| `12(%eax)` | `M[eax+12]` | Access memory at address resulting from `eax + 12`. |
| `(%eax)` | `M[eax]` | Directly access memory at the address contained in `eax`. |
| `3(%eax,%esi,2)` | `M[eax+esi·2+3]` | Access memory at address resulting from `eax + (esi * 2) + 3`. |
| `4` | `M[4]` | Directly access memory at address 4. |
| `$4` | `4` | Immediate value 4. |
| `%eax` | `Registro eax` | Direct reference to the `eax` register. |
| `%al` | `8 bits de menor peso de eax` | Direct reference to the least significant byte of the `eax` register. |

## Sign Extension: `movsbw` Example

- **Source**: `%ch` (byte)
  - Value: `1001 0010` (binary)
  - Decimal: `-110`
- **Destination**: `%ax` (word)

```assembly
movesbw %ch, %ax
```

(`%ax` is now `1111 1111 1001 0010`)

> **Explanation:** We want to move the value of `%ch` ino `%ax`. Since `%ax` holds a word (2 bytes), we have to fill up the left byte of `%ax` to retain `%ch`'s true value. Since the MSB of `%ch` is 1 (negative), we fill up the left byte with 1's.

## Instrucciones Aritmeticas

| Instruction | Description | Notes | Example |
|-------------|-------------|-------|---------|
| `addx op1, op2` | Add `op1` to `op2` and store the result in `op2`. | `x` can be {L, W, B} | `addl $13, %eax` |
| `subx op1, op2` | Subtract `op1` from `op2` and store the result in `op2`. | `x` can be {L, W, B} | `subw %cx, %ax` |
| `adcx op1, op2` | Add `op1` to `op2` along with the carry flag (`CF`) and store the result in `op2`. | `x` can be {L, W, B} | `adcl %edx, %eax` |
| `sbbx op1, op2` | Subtract `op1` from `op2` along with the carry flag (`CF`) and store the result in `op2`. | `x` can be {L, W, B} | `sbbl %ecx, %eax` |
| `incx op1` | Increment `op1` by 1 and store the result in `op1`. | `x` can be {L, W, B} | `incl %eax` |
| `decx op1` | Decrement `op1` by 1 and store the result in `op1`. | `x` can be {L, W, B} | `decw %bx` |
| `negx op1` | Negate `op1` (change the sign) and store the result in `op1`. | `x` can be {L, W, B} | `negl %eax` |
| `imul op1, op2` | Multiply `op1` by `op2` and store the result in `op2`. | \- | `imul (%ebx), %eax` |
| `imul inm, op1, op2` | Multiply `op1` by the constant `inm` and store result in `op2`. | `inm` is a constant | `imul $3, %eax, %ecx` |
| `imull op1` | Multiply `op1` by `%eax` and store result in `%edx:%eax`. | \- | `imull (%ebx)` |
| `mull op1` | Multiply `op1` by `%eax` (unsigned) and store result in `%edx:%eax`. | \- | `mull (%ebx)` |
| `cltd` | Sign-extend `%eax` into `%edx:%eax`. | \- | `cltd` |
| `idivl op1` | Divide `%edx:%eax` by `op1`, result in `%eax`, remainder in `%edx`. | \- | `idivl %ebx` |
| `divl op1` | Divide `%edx:%eax` by `op1`, result in `%eax`, remainder in `%edx`. | \- | `divl %esi` |

## Logical Operations

| Instruction | Description | Example |
|-------------|-------------|---------|
| `andx op1, op2` | Bitwise AND `op1` with `op2` and store the result in `op2`. | `andl $13, %eax` |
| `orx op1, op2` | Bitwise OR `op1` with `op2` and store the result in `op2`. | `orw %cx, %ax` |
| `xorx op1, op2` | Bitwise XOR `op1` with `op2` and store the result in `op2`. | `xorl %edx, %eax` |
| `notx op1` | Bitwise NOT `op1` and store the result in `op1`. | `notb %ah` |
| `salx k, op1` | Arithmetic left shift `op1` by `k` bits and store the result in `op1`. `k` can be an immediate or `%cl`. | `sall $1, %eax` |
| `shlx k, op1` | Logical left shift `op1` by `k` bits and store the result in `op1`. `k` can be an immediate or `%cl`. | `shlw %cl, %dx` |
| `sarx k, op1` | Arithmetic right shift `op1` by `k` bits and store the result in `op1`. `k` can be an immediate or `%cl`. | `sarl $1, %eax` |
| `shrx k, op1` | Logical right shift `op1` by `k` bits and store the result in `op1`. `k` can be an immediate or `%cl`. | `shrw %cl, %dx` |
| `cmpx op1, op2` | Compare `op1` with `op2` and set flags accordingly. The result is not stored. | `cmpl $13, %eax` |
| `testx op1, op2` | Bitwise AND `op1` with `op2` and set flags accordingly. The result is not stored. | `testw %cx, %ax` |

## Sequencing Instructions (Instrucciones de Secuenciamiento)

| Instruction | Description | Notes | Example |
|-------------|-------------|-------|---------|
| `jmp etiq` | Unconditional jump to label `etiq`. |  | `jmp loop` |
| `jmp op` | Unconditional jump to address specified by `op`. | `op` can be a register or memory location. | `jmp (%ebx,%esi,4)` |
| `jcc etiq` | Conditional jump to label `etiq` based on condition `cc`. | `cc` can be conditional flags like `e`, `ne`, `g`, `GE`, `L`, `LE`, etc. | `je else` |
| `jcc etiq` | Conditional jump to label `etiq` based on condition `cc`. | `cc` can be conditional flags like `a`, `ae`, `b`, `be`, etc. | `ja loop` |
| `jcc etiq` | Conditional jump to label `etiq` based on condition `cc`. | `cc` can be conditional flags like `z`, `nz`, `c`, `nc`, `O`, etc. | `jnc error` |
| `call etiq` | Call subroutine at label `etiq`. | Pushes return address onto the stack and jumps to `etiq`. | `call sub` |
| `call op` | Call subroutine at address specified by `op`. | `op` can be a register or memory location. | `call (%ebx)` |
| `ret` | Return from subroutine. | Pops return address from the stack and jumps to it. | `ret` |

## Example: `je` (Jump if Equal)

Suppose we have the following comparison:

```assembly
cmp $10, %eax
je equal_label
```

If the comparison reveals that `%eax` is equal to 10, the je instruction will jump to the `equal_label`. Otherwise, it will continue with the next instruction.

## Flags in Assembly Language

### Zero Flag (ZF)

- **Description**: The Zero Flag (ZF) is set if the result of an operation is zero.
- **Set by**: 
  - In comparison instructions like `cmp` and `test`, ZF is set if the operands are equal.
- **Use**: It's used to check if two values are equal.

**Example**:

```assembly
; Set ZF when comparing equal values
cmpl $10, $10    ; Compare 10 with 10, ZF is set
```

### Carry Flag (CF)

- **Description**: The Carry Flag (`CF`) is set when there is a carry-out (borrow) from the most significant bit during arithmetic operations like addition or subtraction.
- **Set by**: 
  - In `add` and `adc` (add with carry) instructions, `CF` is set if there's a carry from the most significant bit during addition.
  - In `sub` and `sbb` (subtract with borrow) instructions, `cf` is set if a borrow is required from the most significant bit during subtraction.
- **Use**: It's commonly used for unsigned integer overflow detection.

**Example**:

```assembly
; Set CF when adding two large unsigned numbers
addl $4294967295, $1   # $1 + 4294967295 = 0, CF is set
```

### Sign Flag (SF)

- **Description**: The Sign Flag (SF) is set if the result of an operation is negative.
- **Set by**: 
  - In arithmetic instructions, SF is set based on the sign of the result (the most significant bit).
- **Use**: It's used to check the sign of a result.

**Example**:

```assembly
; Set SF when result is negative
subl $5, $10    # Subtract 5 from 10 (result: 5), SF is not set
subl $10, $15   # Subtract 10 from 15 (result: -5), SF is set
```

### Overflow Flag (OF)

- **Description**: The Overflow Flag (OF) is set when there is an arithmetic overflow, which occurs when the result of an operation cannot be represented in the given number of bits.
- **Set by**: 
  - In `add` and `sub` instructions, OF is set if there is a signed overflow.
  - In `inc` and `dec` instructions, OF is set if there is a signed overflow.
- **Use**: It's used to detect signed integer overflow.

**Example**:

```assembly
; Set OF when signed overflow occurs
addl $2147483647, $1   # 2147483647 + 1 = -2147483648 (overflow), OF is set
```

## Data Structures and how to access them

## Vectors

| C Declaration | Element Size | Vector Size | Description |
|---------------|--------------|-------------|-------------|
| char A[12]; | 1B | 12B | Declares an array A consisting of 12 char elements. Each element occupies 1 byte of memory. |
| char *B[80]; | System-dependent | 320B | Declares an array of 80 pointers to char. The size of each pointer depends on the system (e.g., 4 bytes on a 32-bit system). |
| double C[1024]; | 8B | 8KB | Declares an array C consisting of 1024 double elements. Each double typically occupies 8 bytes of memory. |
| int *D[5]; | System-dependent | 20B | Declares an array of 5 pointers to int. The size of each pointer depends on the system. |
| int E[100]; | 4B | 400B | Declares an array E consisting of 100 int elements. Each int typically occupies 4 bytes of memory. |

| Element | Memory Address |
|---------|----------------|
| A[i] | @start A + i |
| B[i] | @start B + 4·i |
| C[i] | @start C + 8·i |
| D[i] | @start D + 4·i |
| E[i] | @start E + 4·i |

### Long example of accessing a vector element

The following is a breakdown of the assembly code for the `Vi` function.

```c
int Vi(int V[100], int i) {
    return V[i];
}
```

```assembly
Vi:
pushl %ebp        # Save the current value of the base pointer (ebp) on the stack.
movl %esp, $ebp
movl 8(%ebp), %ecx # Load the value at address 8 bytes ahead of the base pointer into ecx.
movl 12(%ebp), %edx # Load the value at address 12 bytes ahead of the base pointer into edx.
movl (%ecx,%edx,4), %eax # Calculate the effective address as ecx + 4 * edx and load the value at that address into eax.
popl %ebp         # Restore the original value of the base pointer from the stack.
ret              # Return to the calling function with the value in eax.
```

1. `pushl %ebp`: This instruction saves the current value of the base pointer (ebp) on the stack.(Establishes the stack frame for the current function).
2. `movl %esp, %ebp`: It sets up a new base pointer (ebp) by copying the stack pointer (esp). This is used to create a stable reference point within the function.
3. `movl 8(%ebp), %ecx`: This line loads the value at the memory address located 8 bytes ahead of the base pointer (`ebp`)(starting address of the array `V`) into the `ecx` register.
4. `movl 12(%ebp), %edx`: Similarly, this instruction loads the value at the memory address located 12 bytes ahead of the base pointer (ebp) into the edx register. This is `i`.
5. `movl (%ecx,%edx,4), %eax`: It calculates an effective memory address by adding the values in `ecx` and `edx`. Additionally, it multiplies the value in `edx` by `4` (length of an `int` in C). The result is used as an index to access an integer element in the array `V`. The value at this memory location is loaded into the `eax` register, which is often used to hold function return values. See [here](#vectors) why is is caluclated like that.s
6. `popl %ebp`: This instruction restores the original value of the base pointer (`ebp`) from the stack. It's part of the function's epilogue, which cleans up the stack before returning.
   S
7. `ret`: The `ret` instruction is used to return control to the calling function. The value in `eax` is typically the result.

## Matrix

| C Declaration | Element Size | Total Size | Description |
|---------------|--------------|------------|-------------|
| `char A[80][25];` | 1B | 2000B | 2D array of 80x25 char elements. |
| `char *B[80][10];` | Depends on system | 3200B | 2D array of 80x10 pointers to char. |
| `double C[1024][100];` | 8B | 800KB | 2D array of 1024x100 double elements. |
| `int *D[5][90];` | Depends on system | 1800B | 2D array of 5x90 pointers to int. |
| `int E[100][30];` | 4B | 12000B | 2D array of 100x30 int elements. |

> **Note:** We address the element `M[i][j]` as following:

```C
M[i][j] = @start M + (i * #Columns + j) * LengthOfValues
```

- `@start M` represents the starting memory address of the array `M`.
- `i` is the row index.
- `#Columns` is the number of columns in the array.
- `j` is the column index.
- `LengthOfValues` is the size (in bytes) of each element in the array.

| Array Declaration | Starting Address (Element @ (i, j)) |
|-------------------|-------------------------------------|
| `char A[80][25];` | @inicio A + (i * 25 + j) |
| `char *B[80][10];` | @inicio B + ((i * 10 + j) * 4) |
| `double C[1024][100];` | @inicio C + ((i * 100 + j) * 8) |
| `int *D[5][90];` | @inicio D + ((i * 90 + j) * 4) |
| `int E[100][30];` | @inicio E + ((i * 30 + j) * 4) |

The correspoindig `mov` instructions would look like this:

| Array Declaration | `mov` Instruction for Element @ (i, j) |
|-------------------|--------------------------------------|
| `char A[80][25];` | `mov (%eax, %ebx, 4), %edx`   ; Assuming %eax contains the base address of A and %ebx contains the value of (i * 25 + j) |
| `char *B[80][10];` | `mov (%ecx, %ebx, 4), %edx`   ; Assuming %ecx contains the base address of B and %ebx contains the value of (i * 10 + j) |
| `double C[1024][100];` | `mov (%esi, %ebx, 8), %edx`   ; Assuming %esi contains the base address of C and %ebx contains the value of (i * 100 + j) |
| `int *D[5][90];` | `mov (%edi, %ebx, 4), %edx`   ; Assuming %edi contains the base address of D and %ebx contains the value of (i * 90 + j) |
| `int E[100][30];` | `mov (%ebp, %ebx, 4), %edx`   ; Assuming %ebp contains the base address of E and %ebx contains the value of (i * 30 + j) |

> **Important:** In real code, we first have to write the address of our data structure (e.g. `A`) into the value of the first argument (`base address`, index, scalar). Also the value in the second argument has to contain the offset to the index we are adressing (base address, `index`, scalar). Lastly, we have to indicate the lenght of our elements using the third argument to correctly compute our offset (base address, index, `scalar`).

### Long example of accessing a matrix element

The following is a breakdown of the assembly code for the `Vi` function.

```c
int Mfc(int M[50][80], int fil, int col) {
    return M[fil][col];
}
```

```assembly
Mfc:
pushl %ebp           # Save the current value of the base pointer (ebp) on the stack.
movl %esp, %ebp      # Set up a new base pointer (ebp) by copying the stack pointer (esp).

imull $80, 12(%ebp), %eax  # Multiply the value of 'fil' by 80 and store the result in eax. This computes the offset within the row.
addl 16(%ebp), %eax  # Add the value of 'col' to eax. This computes the final offset within the row.
movl 8(%ebp), %ecx    # Load the address of the 2D array 'M' into ecx.
movl (%ecx,%eax,4), %eax  # Dereference the address (ecx + eax * 4) to access the integer element in the 2D array 'M' and store it in eax.

popl %ebp            # Restore the original value of the base pointer from the stack.
ret                  # Return to the calling function with the value in eax.
```

1. `pushl %ebp`: Saves the current value of the base pointer (ebp) on the stack.
2. `movl %esp, %ebp`: It sets up a new base pointer (ebp) by copying the stack pointer (esp). Creates a stable reference point.
3. `imull $80, 12(%ebp), %eax`: Multiply the value of 'fil' (which is located at 12 bytes ahead of the base pointer) by 80 and store the result in eax. This calculation computes the offset within the row. See [here](#matrix)
4. `addl 16(%ebp), %eax`: Add the value of 'col' (which is located at 16 bytes ahead of the base pointer) to eax. This computes the final offset within the row.
5. `movl 8(%ebp), %ecx`: Load the address of the 2D array 'M' into ecx. This is the base address of the array.
6. `movl (%ecx,%eax,4), %eax`: Dereference the address (ecx + eax * 4) to access the integer element in the 2D array 'M' and store it in eax. The calculation is explained [here](#matrix).
7. `popl %ebp`: This instruction restores the original value of the base pointer (ebp) from the stack.
8. `ret`: Finally, the ret instruction returns eax to the caller.

## 3D Matrix

For example:

```C
int M3D[10][64][48];
```

We can obtain the elements as following:

```css
M3D[i][j][k] = @start M3D + (layer * #rows * #columns + row * #columns + column) * lengthOfValue
```

> **Hence:** In assembly, we would therefore need two `imull` instructions and two `addl` instructions in order to obtain the offset.

cara = layer

## Translation Examples

### Initialize data and run sum over matrix (Estudio Previo L3/1)

```C
#define N 10
int Matriz[N][N],i,suma;
for (i=0,suma=0;i<N;i++)
suma+=Matriz[i][2];
```

```assembly
.data
    N equ 10                  ; Equivalent of #define in C
    Matriz: .skip N*N*4       ; Reserve space for a 10x10 matrix of double words (integers)

.text
.globl _start
_start:
    movl $0, %eax     # i = 0
    movl $N, %esi     # N = 10 (move directly, don't dereference)
    movl $0, %ebx     # suma = 0
    leal Matriz, %edx # Load address of Matriz into %edx

.bucla: 
    cmpl %esi, %eax    # if %esi - %eax <= 0 
    jge .done        
    imull $N, %eax, %ecx  # multiply i by 10
    addl $2, %ecx        # For the offset of j
    addl (%edx, %ecx, 4), %ebx  # M[i][j] = @Matriz + (i * #Columns + j) * LengthOfValues
    incl %eax            # Increment i
    jmp .bucla

.done:
    movl %ebx, %eax
```

### Running sum of matrix sequentially (Estudio Previo L3/2)
In this example, we translate the same code from the previous example, however, we run the sum sequetially by moving our pointer row by row.

```C
#define N 10
int Matriz[N][N],i,suma;
for (i=0,suma=0;i<N;i++)
suma+=Matriz[i][2];
```

Initial position of pointer **P**:

```css
0 P 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0
. . . . . . . . . .
```

Position of pointer **P** after first iteration:

```css
0 0 0 0 0 0 0 0 0 0
0 P 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0
. . . . . . . . . .
```

```assembly
.data
    N equ 10                  # Equivalent of #define in C
    Matriz: .skip N*N*4       # Reserve space for a 10x10 matrix of double words (integers)

.text
.globl _start
_start:
    movl $0, %eax     # i = 0
    movl $N, %esi     # N = 10 (move directly, don't dereference)
    movl $0, %ebx     # suma = 0
    leal Matriz, %edx # Load address of Matriz into %edx
    addl $2*4, %edx   # Directly move to the 3rd element of the first row

.bucla: 
    cmpl %esi, %eax    # if %esi - %eax <= 0 
    jge .done        
    addl (%edx), %ebx  # Add the value at the current memory location to %ebx (i.e., suma)
    addl $N*4, %edx    # Move to the third element of the next row (skipping ahead N elements)
    incl %eax          # Increment i
    jmp .bucla

.done:
    movl %ebx, %eax
```

> **Note:** Not only we reduced the instructions compared to the example above, we also avoided the use of `imull`, which is costly.

## Example of working with multiple data sources
In this example, we initialize each element of `ResFila` to 1. Then for each row in `Matriz`, we checks every element until a 0 is encountered. If any element in the row is greater than 100 (M), we subtracts that element from the corresponding value in `ResFila`. If a row starts with 0, its corresponding value in `ResFila` remains 1.

```C
#define N 10
#define M 100
int Matriz[N][N],i,j,ResFila[N];
for (i=0,j=0,ResFila[0]=1;i<N;i++,j=0,ResFila[i]=1)
while(Matriz[i][j]!=0) {
if (Matriz[i][j]>M)
ResFila[i]-=Matriz[i][j];
j++;
}
```

```assembly
.data
    N equ 10
    M equ 100
    Matriz: .skip N*N*4          # Reserve space for a 10x10 matrix of integers
    ResFila: .skip N*4           # Reserve space for a 1x10 array of integers

.text
.globl _start
_start:
    movl $0, %eax                # i = 0
    movl $0, %ebx                # j = 0
    leal ResFila, %edi           # Load address of ResFila into %edi

initialize_resfila:
    movl $1, (%edi)              # ResFila[i] = 1
    leal Matriz(, %eax, 4), %edx # Point %edx to the start of row i in Matriz
    addl %ebx, %edx              # Add j offset

while_loop:
    cmpl $0, (%edx)              # Check if Matriz[i][j] is 0
    je next_row

    cmpl $M, (%edx)              # Check if Matriz[i][j] > M
    jle increment_j

    subl (%edx), (%edi)          # ResFila[i] -= Matriz[i][j]

increment_j:
    incl %ebx                    # j++
    addl $4, %edx                # Move to the next column in the row
    jmp while_loop

next_row:
    addl $4, %edi                # Move to the next element in ResFila
    incl %eax                    # i++
    testl %eax, %eax
    jge finish
    movl $0, %ebx                # j = 0
    jmp initialize_resfila
```

## Data Alignment (32-bit)
### Structs
![Data Alignment of a struct in 32bit system](./figures/alignment.png)
### Example of working with structs 
Given the following struct `elem` and the declaration of `s`:
```C
typedef struct{
  char a;
  int b[10];
} elem;

elem s[100];
```
```css
+-------------------+
|         a         |  1 byte
+-------------------+
|    -----------    |  Padding
+-------------------+
|    -----------    |  Padding
+-------------------+
|    -----------    |  Padding
+-------------------+
|       b[0]        |  4 bytes
+-------------------+
|       ...         |
+-------------------+
|       b[9]        |  4 bytes
+-------------------+
```
> **Note:** We have to add paddings under `int a`, because the starting address of the structs fields and the size of the structure must be a multiple of 4.
### GCC IA32 data type lengths
| Data Type  | Size (bytes)  | Description                           |
|------------|--------------|---------------------------------------|
| `char`     | 1            | Character                              |
| `int`      | 4            | Integer                                |
| `float`    | 4            | Single-precision floating point       |
| `double`   | 8            | Double-precision floating point       |
| `short`    | 2            | Short integer                          |
| `long`     | 4 (32-bit)   | Long integer   |
| `unsigned` | Varies       | Unsigned integer (depends on system)  |
| `bool`     | 1            | Boolean (true/false)                   |


### Addressing fields of the struct
```css
@s[i].b[j] = @s + (Size of elem * i) + Offset of b in elem + (Size of int * j)
```
Or concretly:
```css
@s[i].b[j] = @s + (44 * i) + 4 + (4 * j)
```
### Addressing fields of the struct in assembly
```C
x = s[s[i].b[j]].a
```
Given 
-    @s is in `%ebx`.
-    i is in `%esi`.
-    j is in `%edi`.
-    x is in `%dl`.
```assembly
# Calculate the address of s[i].b[j]
  imull $44, %esi, %eax     # Multiply i by size of elem (44 bytes)
  addl %ebx, %eax           # Add the base address of s
  addl $4, %eax             # Add offset for 'a' (4 bytes)
  imull $4, %edi, %ecx      # Multiply j by size of int (4 bytes)
  addl %ecx, %eax           # Add the offset for b[j]

# Fetch the value from s[i].b[j] to use as an index for s[...].a
  movl (%eax), %eax         # Load the value of s[i].b[j] into %eax

# Calculate the address of s[...].a
  imull $44, %eax, %eax     # Multiply the fetched value by size of elem (44 bytes)
  addl %ebx, %eax           # Add the base address of s

# Store the result in x
  movb (%eax), %dl          # Load the value of s[s[i].b[j]].a into dl (x)
```

## Example Lab3 Task 1
### Setting up the Stackframe
This example shows how the stackframe of the following code is set up by the calling function:
```C
# Which initialises int i and int sum in this order. 
int OperaVec(int Vector[], int elementos);
```
- The calling function sets up the parameters below the return address. 
- `pushl	%ebp` We save the current base pointer 
- `movl	%esp, %ebp` We move the stack pointer to `%ebp` to get a consistent point of reference 
- `subl	$16, %esp` We have to allocate space for our local variables. The fist one declared in the code will be on top of the frame. !!Question: In the given code, why do we allocate 16 bytes if we only have 2 ints?!!
- `pushl	%ebx` Save the registers
- `pushl	%esi`
- `pushl	%edi`

```css
+-------------------+  <-- %esp - 16 (??)
|       ...         |  
+-------------------+  <-- %ebp - 8
|        i          |  
+-------------------+  <-- %ebp - 4
|       res         |  
+-------------------+  <-- %ebp
|   previous %ebp   |  
+-------------------+  <-- %ebp + 4
|   @return         |  
+-------------------+  <-- %ebp + 8
|     @Vector       |  
+-------------------+  <-- %ebp + 12
|    elementos      |  
+-------------------+
```
> **Figure:** This represents the stackframe after it has been setup.

### Regeisters that have to be stashed by the subroutine
pushl	`%ebx`, `%esi` and `%edi` have to be stashed before the execution of the subroutine and subsequently restored before returning

### Implementation of OperaVec
This is a plain implementation of the `OperaVec` function. The next section includes an optimized verion.
```C
int res;
for (i=1; i<elementos; i++)
  if (Vector[i]==Vector[i-1])
  res=i
```
```assembly
	  movl $1, -8(%ebp)				  # Init i to 0
	  movl 8(%ebp), %ecx				# Move address of v[] to ecx
.loop:
	  movl -8(%ebp), %esi				# Move i into register esi
	  cmpl 12(%ebp), %esi				# Compare i and elementos (i - elementos)
	  jge .done						# Finish if zero flag is set

	  leal (%ecx, %esi, 4), %eax		# Load address of v[i] into %eax
	  movl (%eax), %edx				# Load value into edx

	  decl %esi
	  leal (%ecx, %esi, 4), %ebx		# Load address of v[i-1] into %ebx
	  movl (%ebx), %edi	

	  incl %esi						# Increment i back to real value
	  cmpl %edx, %edi					# Compare v[i] with v[i-1]
	  jne .notEqual					# Jump if Zero flag is not set
	  movl %esi, -4(%ebp)				# Move i into res
.notEqual:
	  incl -8(%ebp)					# Increment i
	  jmp .loop						# Jump back into loop
.done:
```
### Optimized Implementation of OperaVec
This example includes an optimized implementation of the one above
```assembly
    movl $1, -8(%ebp)				# Init i to 0
	movl 8(%ebp), %ecx				# Move address of v[] to ecx
```
> **Note:** The first block remains the same
```assembly
.loop:
	movl -8(%ebp), %esi				# Move i into register esi
	cmpl 12(%ebp), %esi				# Compare i and elementos (i - elementos)
	jge .done						# Finish if zero flag is set

	leal (%ecx, %esi, 4), %eax		# Load address of v[i] into %eax
```
> **Note:** Here we save a `movl` by just dereferecing the address in the `cmlp` later.
```assembly
	  leal -4(%ecx, %esi, 4), %edi	# Load address of v[i-1] into %ebx
	movl (%edi), %edi				# Load value of v[i-1] into edi
```
> **Note:** We reuse the `%edi` register so it serves a single purpose.	  
```assembly    
    cmpl (%eax), %edi				# Compare v[i] with v[i-1] 
	jne .notEqual					# Jump if Zero flag is not set
	movl %esi, -4(%ebp)				# Move i into res
.notEqual:
	incl -8(%ebp)					# Increment i
	jmp .loop						# Jump back into loop
.done:
```
Although the speed up is minor, the second implementation is more optimized and efficient. It uses fewer registers and combines the address calculations in a more concise manner.

## TODO: Insert L3 Task 2 (Matrix)
```C
res=0;
for (i=0; i <3; i+=salto)
  for (j=0; j <= i; j++)
    res+=Matriz[i][j];
```
```assembly
movl $0, -4(%ebp)				# Move 0 to res
	movl $0, -8(%ebp)				# Move 0 to i
	movl 8(%ebp), %ecx				# Move @M to ecx
	movl 12(%ebp), %edx				# Move salto into register

.outer: 
	movl -8(%ebp), %esi				# Move i to reg esi
	cmp  $3, %esi					# Compare i with 3. i - 3
	jge .done 						# Jump to done if i -3 = 0
	movl $0, -12(%ebp)				# Set j to 0
.inner:
	cmpl %esi, -12(%ebp)			# Compare i and j, j - i
	jg .incrementi
	imull $3, %esi, %edi			# Calculate offset for i
	addl -12(%ebp), %edi			# Add value of j to offset
	leal (%ecx, %edi, 4), %edi 		# Move address of M[i][j] into %esi, reconsider if this is smart
	movl (%edi), %edi				# Move value into reg
	addl %edi, -4(%ebp)				# Add M[i][j] to res
	incl -12(%ebp)
	jmp .inner

.incrementi:
	addl %edx, -8(%ebp)
	jmp .outer

.done:
```
## Example of an Activation Block
If we want to call a function, we have to set up its activation block correctly. This includes pushing the required arguments on the stack before we `call` the routine. 
```C
void PDOT(int M[10][10], int *p) {
  int i;
  *p = 0;
  for (i=0; i<10; i++)
    *p += DOT(&M[0][0],&M[i][0],10);
}
```
The lower part of this figure represents the activation block of the `PDOT` routine. The upper part (starting from ebp -4) is set up by the `PDOT` routine represents the activation block of `DOT`. 
```css
+-------------------+
|       ...         |
+-------------------+  <-- esp (after arguments are pushed for DOT)
|    &M[0][0]       |  
+-------------------+
|    &M[i][0]       |
+-------------------+
|       10          |
+-------------------+  <-- ebp - 4
|       i           |   
+-------------------+  <-- ebp
|   Previous EBP    |   
+-------------------+  <-- ebp + 4
|      @Return      |   
+-------------------+  <-- ebp + 8 
|     M[10][10]     |  
+-------------------+  <-- ebp + 12
|       @p          |   
+-------------------+
|       ...         |
+-------------------+
```
The corresponding assembly to set this up looks like this:
```assembly
  pushl $10
  imull $10,-4(%ebp),%edx
  movl 8(%ebp),%ebx
  leal (%ebx,%edx,4),%eax
  pushl %eax
  pushl %ebx
  call DOT
```
# Tema 3: Jerarquía de Memorias
## Temporal Locality
**If we access a memory position, it is very likely that we will access the same position again in the near future.**

**Why? Because of loops.**
- **Instructions:** Within a loop, the same instructions are accessed repeatedly.
- **Data:** Within a loop, the same variables are accessed repeatedly.

---

## Spatial Locality
**If we access a memory position, it is very likely that we will access nearby positions in the near future.**

**Why?**
- **Instructions:** Instructions are executed in sequence.
- **Data:** Vectors and matrices are usually traversed in sequence; parameters and local variables are in the subroutine's activation block.
## Cache Memory
In any Cache Memory, the following must be defined:
- **Placement Algorithm:** Determines in which cache memory lines a block can be placed. It also determines where to search for data.
- **Replacement Algorithm:** Determines which line should be removed from the cache to make space for a new block.
- **Writing Policies:** Determines how writes are performed. In any case, in the end, it always has to be written in the main memory (MP).
- These must be hardware algorithms:
  - Simple algorithms.
  - Fast algorithms.

## Placement Algorithms
### Direct Mapping
- Each block of main memory maps to a specific line in the cache.
- Determined by: `Cache Line = Memory Block mod Number of Cache Lines`
### Set-Associative
- Cache is divided into several sets, and each set contains a number of lines.
- A block of main memory can be placed in any line within a specific set.
- Determined by: `Cache Set = Memory Block mod Number of Sets`
- Combines features of both Direct Mapping and Fully Associative.

### Fully Associative
- Any block of main memory can be placed in any line of the cache.
- No restrictions on placement, but requires more complex hardware to search the cache.


## Examples of Placements
![Chache Placements](./figures/cache-placement.png)

### 1. Direct Mapping (`Emplazamiento DIRECTO`)
- Every main memory block has a specific cache line.
- Formula: `Línea MC = Bloque de memoria mod #líneas MC`

**Cache Line Format**:
- `TAG`: Identifier for the main memory block.
- `#línea MC`: Cache line number.
- `#byte`: Data stored.

### 2. Set Associative Mapping (`Emplazamiento ASOCIATIVO por CONJUNTOS`)
- Cache is divided into sets; each set contains multiple lines.
- A memory block can be placed in any line within its designated set.
- Formula: `Conjunto MC = Bloque de memoria mod #Conjuntos`

**Cache Line Format**:
- `TAG`: Identifier for the main memory block.
- `#conj. MC`: Set number.
- `#byte`: Data stored.

### 3. Fully Associative Mapping (`Emplazamiento COMPLETAMENTE ASOCIATIVO`)
- A memory block can be placed in any cache line.
- No specific placement formula.

**Cache Line Format**:
- `TAG`: Identifier for the main memory block.
- `#byte`: Data stored.

### [Vorlesung KIT](https://www.youtube.com/watch?v=qWVKwo0EhSY)
## Some cache formulas
### Average Memory Access Time for Instruction Accesses
$$ TmaI = Tsa + m \times Tpf $$

Where:
- $Tsa$: Service time in case of a hit.
- $m$: Miss rate for instructions.
- $Tpf$: Penalty for a cache miss.

### Average Memory Access Time for Data Accesses

$$ TmaD = Tsa + m \times ( (1-pm) \times Tpf_{unmodified} + pm \times Tpf_{modified} ) $$

Where:
- $Tsa$: Service time in case of a hit.
- $m$: Miss rate for data.
- $pm$: Percentage of modified blocks (as a fraction).
- $Tpf_{unmodified}$: Penalty for replacing an unmodified block.
- $Tpf_{modified}$: Penalty for replacing a modified block.

### Average Memory Access Time for All Accesses

$$ Tma = \frac{(TmaI \times ref_{inst} + TmaD \times ref_{data})}{ref_{inst} + ref_{data}} $$

Where:
- $TmaI$: Average memory access time for instruction accesses.
- $TmaD$: Average memory access time for data accesses.
- $ref_{inst}$: Number of references for instruction.
- $ref_{data}$: Number of references for data.

### Time per instruction
$$
T_{\text{exec}} = (CPI + nr \times T_{\text{ma}}) \times T_c
$$

Where:
-  $T_{\text{exec}}$  : Execution time of one instruction
-  $CPI$  : Cycles per instruction
-  $nr$ : Number of references per instruction
-  $T_{\text{ma}}$ : Average memory access time
-  $T_c$ : Cycle time

### Total CPI
$$
CPI_{\text{total}} = CPI_{\text{base}} + \frac{\text{Penalización por fallo de caché} \times \text{Número de fallos de caché}}{\text{Número total de instrucciones}}
$$

### Number of Cache Sets and Rows per Set
Given a cache size \( S \) and block size \( B \), the number of blocks \( m \) is:
$$
m = \frac{S}{B}
$$
For an n-way set associative cache, the number of sets is:
$$
\text{Number of Sets} = \frac{m}{n}
$$
And the number of rows per set (or blocks per set) is \( n \).

### Blocks per Way:
Blocks per way is the number of cache blocks divided by the number of ways.
$$
\text{Blocks per Way} = \frac{\text{Number of Cache Blocks}}{\text{Number of Ways}}
$$

### Byte Offset
To determine the block offset, which represents the number of bits needed to address a specific byte within a block:
$$
\text{Offset} = \log_2(\text{Block size})
$$


### Set Index Offset
$$
\text{Set Index} = \log_2(\text{Number of Sets})
$$

### Set Mapping of Blocks
To determine which set a particular block maps to:
$$
\text{Set number} = \text{Block number} \mod \text{Number of Sets}
$$

### Size in bits of the data memory and the tag memory of one way

To calculate the size of the data memory $T_{\text{datos}}$ and the tag memory $T_{\text{etiquetas}}$ for one way, we use the following formulas:

#### Data memory size:
$$
T_{\text{datos}} = \text{Blocks per way} \times \text{Block size in bytes} \times 8 \text{ bits/byte}
$$

#### Tag memory size:
$$
T_{\text{etiquetas}} = \text{Blocks per way} \times \text{Tag bits per block}
$$

Where:
- **Blocks per way** is the number of cache blocks assigned to one way.
- **Block size in bytes** is the amount of bytes in each cache block.
- **Tag bits per block** is the number of bits used for the tag of each block.

### Average Dynamic Power (!!!):
The average dynamic power due to switching is calculated using the formula:
$$
P_{\text{dynamic}} = C \times V^2 \times f
$$
Where:
-  C  is the capacitive load
-  V is the voltage
-  f is the frequency

### Average Static Power (!!!):
The average static power due to leakage is calculated as:
$$
P_{\text{static}} = I_{\text{leakage}} \times V
$$
Where:
- $I_{\text{leakage}}$ is the leakage current

### Average Total Power (!!!):
The average total power is simply the sum of the dynamic and static power:
$$
P_{\text{total}} = P_{\text{dynamic}} + P_{\text{static}}
$$

### Power of a CPU-Cache system
$$
P_{\text{total}} = CPU_{\text{static}} + CPU_{\text{dynamic}} + Cache_{\text{static}} + Cache_{\text{dynamic}}
$$
Where:
-  $CPU_{\text{static}}$ is the static power of the CPU
-  $CPU_{\text{dynamic}}$ is the dynamic power of the CPU
-  $Cache_{\text{static}}$ is the static power of the Cache (Tag and Data cache!!)
-  $Cache_{\text{dynamic}}$ is the dynamic power of the Cache (Tag and Data cache!!)
> **Note:** When calculating the cache consumption, it is important to consider the cache configuration (n-way, parallel, serial, predictive)


### Energy Consumption
$$
\text{Energy (in joules)} = \text{Power (in watts)} \times \text{Time (in seconds)}
$$
### Concepts and considerations
#### LRU (Least Recently Used)
LRU is a cache replacement policy that replaces the least recently used block when a new block needs to be loaded into the cache. 
- **Example**: If the cache sets are ordered as [A, B, C] with C being the least recently used, and a new block D is accessed which is not in the cache, then the cache will update to [D, A, B].

#### Copy Back + Write Allocate
- **Copy Back**: When data is written to a cache block, the corresponding block in main memory is not immediately updated. Instead, a dirty bit is set for the cache block indicating that its content has changed. The block is written back to main memory only when it's replaced.
  - **Example**: If a write operation occurs on block A in the cache and A's dirty bit is set, the data will not be immediately written to main memory. Only when A is replaced will the data be written back if the dirty bit is 1.

- **Write Allocate**: If a write miss occurs, the block is loaded into the cache, and then the write is performed.
  - **Example**: If a write operation is directed to block B which is not in the cache, block B will first be loaded into the cache, and then the write will be performed on the cache block.

### Memory Access
- **Read from MP**: Occurs when there's a cache miss during a read operation. The required block is fetched from main memory and loaded into the cache.
  - **Example**: Reading address `lect 32C07` resulted in a cache miss, so block `32C` was fetched from main memory.

- **Write to MP**: Occurs under two conditions:
  1. During a write miss when using a write-through policy.
  2. When a block with a dirty bit set to 1 is replaced from the cache.
  - **Example**: Writing to address `escr 72509` resulted in a cache miss. Since the replaced block had a dirty bit of 0, there was no write back to main memory.

- **Performance**: 
  - **Write Back** offers better performance by reducing writes to main memory, especially beneficial when a memory location is frequently written to.
- **Consistency**: 
  - **Write Through** ensures the main memory is always consistent, ideal for multiprocessor systems.

## Virtual Memory: Overview and Performance
Virtual memory is a memory management capability of an operating system (OS) that uses hardware and software to allow a computer to compensate for physical memory shortages, by temporarily transferring data from random access memory (RAM) to disk storage. This process is often entirely transparent to the user.

### Why?

- Multiuser and Multiprogramming Systems: In systems where multiple programs run concurrently, the required memory size can significantly exceed the available physical memory. Virtual memory allows these systems to handle large, concurrent workloads effectively.

- Efficient Use of Memory: Only a small portion of memory is actively used at any given time. Virtual memory ensures that this active portion is kept in physical memory for quick access.

- Program Execution with Limited Physical Memory: It enables the execution of programs that require more memory space than what is physically available.

- Protection and Isolation: Virtual memory provides a mechanism to protect and isolate the address space of different programs, preventing them from accessing each other's memory.

### How Configurations Affect Performance

- Translation Lookaside Buffer (TLB): A special cache used to speed up address translation. The efficiency of the TLB can significantly impact overall system performance.

- Page Size: The size of pages can affect the performance, with trade-offs between smaller pages (reducing memory wastage) and larger pages (reducing the overhead of managing numerous pages).

- Table of Pages: The implementation of the page table, whether single-level or multi-level, and its size can influence the speed of address translation.

### Important Formulas and Examples
#### Virtual Page Number (VPN) to Physical Page Number (PPN) Translation

**Basic Concept**: The logical address space is divided into fixed-size blocks called pages, and the physical memory is divided into frames of the same size. The translation mechanism maps these virtual pages to physical frames.

**Example**: In a system with 64-bit virtual addresses and 43-bit physical addresses, and a page size of 8 KB:

- VPN Size Calculation:
  $$ \text{log2}(8 \times 1024) = 13 \text{ bits for the offset.} $$
  Therefore, VPN size = 64 - 13 = 51 bits.

- PPN Size Calculation:
  Assuming 30 bits are needed for the PPN.
  Therefore, PPN size = 43 - 13 = 30 bits.

#### Address Translation with TLB

**Example Setup**:
- 32-bit logical address, 28-bit physical address.
- Page size: 4KB (2^12 bytes).
- TLB with 4 entries.

**TLB Entry Structure**:
- VPN (20 bits), PPN (16 bits), Validity Bit.

**Translation Process**:
The TLB is checked for a valid entry matching the VPN. If found (hit), the corresponding PPN is used. If not (miss), a page table lookup is performed.

## Conceptos Avanzados de Memoria Cache
## 1-13
- Cache Size and Access Time: Smaller caches reduce access time but might increase the rate of cache misses. Larger caches improve capacity but can slow down access time.
- Cache Optimization Techniques: Techniques like way prediction, trace caches, and non-blocking caches are used to optimize cache performance.
- Cache Associativity: Higher associativity reduces conflict misses but can increase access time.
- Multilevel Caches: Using small L1 caches (faster access, higher miss rate) and large L2 caches (slower access, lower miss rate) balances performance.
- Write Buffers and Prefetching: These techniques are used to reduce the rate of cache misses and the penalty of cache misses.

## Miss categories
The cache misses can be divided into three categories:
- **Compulsory (Load):** Occur the first time a memory location is accessed.
- **Capacity:** All the lines a program needs do not fit in the Cache Memory.
- **Conflict:** Occur when multiple blocks are mapped to the same place in the Cache Memory (only in direct-mapped and set-associative caches).
- **Coherence misses** (In multiprocessors)

## Metrics and how to improve them
### Execution Time Optimization
The final goal of any optimization is to reduce the execution time:
$$
T_{\text{exe}} = N \cdot CPI \cdot T_c
$$
$$
T_{\text{exe}} = N \cdot (CPI_{\text{id}} + CPI_{\text{mem}}) \cdot T_c
$$
$$
T_{\text{exe}} = N \cdot (CPI_{\text{id}} + n_r \cdot m \cdot t_{\text{pf}} + CPI_{\text{WR}}) \cdot T_c
$$

Where:
- $T_{\text{exe}}$ : Execution time
- $N$ : Number of instructions
- $CPI$ : Cycles Per Instruction
- $T_c$ : Cycle time
- $CPI_{\text{id}}$ : Ideal CPI
- $CPI_{\text{mem}}$ : CPI due to memory
- $n_r$ : Number of references per instruction
- $m$ : Miss rate
- $t_{\text{pf}}$ : Penalty time per miss
- $CPI_{\text{WR}}$ : CPI due to write operations

### Memory Hierarchy Influence
- Machine language elements ($N$, $n_r$) are not influenced by the memory hierarchy.
- The memory hierarchy can influence:
  - Miss rate (goal: reduce $m$)
  - Penalty time per miss (goal: reduce $t_{\text{pf}}$)
  - Cost of write operations (goal: reduce $CPI_{\text{WR}}$)
  - Memory bandwidth
### Advanced Memory Hierarchy Concepts: Cache Memory

#### Techniques to Improve Cache Performance
- **Increase Block Size ($m \downarrow$):** Reduces compulsory misses, but can be counterproductive ($m \uparrow$).
- **Increase Cache Size ($m \downarrow$):** Reduces capacity (and conflict) misses, but increases cache access time ($t_{\text{sa}} \uparrow$) and power consumption ($W \uparrow$).
- **Increase Associativity ($m \downarrow$):** Reduces conflict misses, but increases cache access time ($t_{\text{sa}} \uparrow$).
- **Multi-level Caches ($t_{\text{pf}} \downarrow$):** Small L1 (increases $m$ and decreases $t_{\text{sa}}$) and large L2 (decreases $m$ and increases $t_{\text{sa}}$).
- **Prioritize Reads over Writes ($CPI_{\text{WR}} \downarrow$):** The cost of writes can be reduced (hidden) using write buffers.

#### Advanced Techniques for Cache Performance Enhancement
- **Reduce Cache Hit Cost ($t_{\text{sa}} \downarrow$):** Small and simple caches, way prediction, and trace caches.
- **Increase Cache Bandwidth ($BW \uparrow$):** Segmented caches, multi-bank caches, and non-blocking caches.
- **Reduce Miss Penalty ($t_{\text{pf}} \downarrow$):** Early restart and merging write buffers.
- **Reduce Miss Rate ($m \downarrow$):** Compiler optimizations.
- **Reduce Miss Penalty ($t_{\text{pf}} \downarrow$) and Miss Rate ($m \downarrow$) via Parallelism:** Hardware prefetching and software prefetching.

## Way Prediction in Cache Memory
Way prediction is a technique in set-associative cache architectures to improve performance and reduce power consumption.

### Set-Associative Cache
- **Structure**: Multiple "ways" or "lines" in each cache set.
- **Challenge**: Checking all ways for data is time-consuming and energy-intensive.

### Way Prediction Mechanics
1. **Prediction Mechanism**: Uses historical access patterns to predict which way might contain the requested data.
2. **Accessing Data**: Initially accesses only the predicted way.
3. **Updating Prediction**: Adjusts based on actual access outcomes.

### Advantages
- **Reduced Access Time**: Faster data access on correct predictions.
- **Lower Power Consumption**: Less energy used by accessing fewer ways.

### Cache Types with Way Prediction
- **Sequential Access Cache**: Slower, more power-efficient.
- **Parallel Access Cache**: Faster, less power-efficient.

### TODO: 050 Cache avanzada
Folie 17-35

## RAM
### Addresses
RAM is always structured the same (square):
Therefore, for addresses of $\text{n}$ (in bits) we can have:
$$
\#Columns = \#Rows =  2^\frac{\text{n}}{\text{2}} 
$$

### Read Access
#### Row (Fila) via wordline
First $\frac{\text{n}}{\text{2}}$ bits of a address.
> **Note:** All the cells in this row are accessed, the data from the entire row is sent to the signal amplifiers, and the voltage is recovered.

#### Column via bit line
Remaining bits of the address.
Decode @COLUMN, select a bitline, and send the data to the R/W buffer.
> **Note** The reading is destructive, it is necessary to rewrite the cell (and the entire row) to recover the original value and precharge the bitlines for the next memory access.

### Write Access
Practically the same, the only difference is that the cell is rewritten with the data that enters through the R/W buffer.
> **Note** It is necessary to rewrite the cell with the new value and the rest of the row with the original value.

### Process Synchronization Chronogram for DRAM
![Chronogram DRAM](./figures/dram_signal.png)
- Once the `RAS` signal goes to zero, it triggers `A` (Address bus)
- **1. )Decode Row (@FILA)**:
    The Row Address Strobe (RAS) signal is activated to select the row in the DRAM matrix where the data will be accessed.
    The address lines (A) are used to specify which row (also known as a page) is to be accessed.
- **2.) Access Page:**
    The selected row's data is loaded into the row buffer, making it ready for read or write operations.
    This stage involves activating the sense amplifiers to read the entire row from the array into the row buffer.
    > Once it is loades, the `CAS` signals goes off and triggers the loading og the column in the same bus.
- **3.) Decode Column (@COLUMNA):**
    The Column Address Strobe (CAS) signal is activated to select the specific column within the already selected row.
    The address lines now carry the column address to pinpoint the exact cell (or cells, in case of a burst read/write) for the operation.
- **4.) Data Transfer:**
    The data line (D) is now active, indicating the transfer of data.
    If it's a read operation, data from the selected cell is output to the data bus.
    If it's a write operation, data from the data bus is written into the selected cell.
    > Data is loaded using the data bus `D`
    > The `RDY` signal is switched on, as the data is ready.
    > The `RAS` and the `CAS` signals are also switched on until the next address is read 
- **5.) Precharge Page:**
    After the read or write operation, the row needs to be precharged before it can be accessed again.
    This involves resetting the sense amplifiers and preparing the DRAM row for the next access.

### Timings
![Timings](./figures/timings.png)

- **Access Time ($T_{\text{RAC}}$):** The maximum delay from when the row address is supplied until the data is obtained, which corresponds to the memory latency.

- **Cycle Time ($T_{\text{RC}}$):**
The minimum time interval between two consecutive memory accesses, which relates to bandwidth.

- **Column Access Time ($T_{\text{CAC}}$):**
The maximum delay from when the column address is supplied until the data is obtained.
### Access protocols and "column caching"
### Asynchronous Memory

- **Timing**: Asynchronous memory does not synchronize with the system clock. Access times are not tied to a specific clock frequency, and each action starts independently of a clock signal.
- **Control Signals**: It uses control signals, such as WE (Write Enable), OE (Output Enable), and CE (Chip Enable), without relying on a clock.
- **Latency**: Latency in asynchronous memory can vary, as it is not tied to a clock cycle. The access time is determined by the duration of the control signal.
- **Speed**: Generally slower than synchronous memory due to the lack of coordination with the CPU's clock, which can lead to wait states where the CPU must wait for the memory.


### Synchronous Memory

- **Timing**: Synchronous memory, as the name suggests, is synchronized with the system clock. All operations (read, write, refresh) occur on a specific edge of the clock cycle.
- **Control Signals**: It uses commands like ACT, READ, WRITE, and PRE, which are issued on clock edges. The memory controller must wait for the right clock edge to issue commands.
- **Latency**: Latency is defined in clock cycles (such as CAS latency), and operations are predictable, which allows for more efficient scheduling of memory access.
- **Speed**: Faster than asynchronous memory due to synchronization with the system clock.
- **Examples**: DDR (Double Data Rate) SDRAM, DDR2, DDR3, DDR4, and so on.

### Reusing the @FIL
Enhance spacial locality by saving `@FIL` for subsequent `@ COL` reads, since they likly will be consecutive. 
> **Enhancement:** We just have to update `@COL`

### Reusing the @COL
- **Problem:** It is necessary to wait for the data to be read before sending the new `@COL`

- **Solution:** A register is added at the data output
which allows the overlap of data access with the sending of the new `@COL`. We add a counter to automatically generate `@COL+1`, `@COL+2`, and `@COL+3`.

- **Result:** Since the data is stored in a register, before the data transmission is completed, we can already send the `@COL`. In the case of the counter, we just send it once and then add the offset for future transmissions.

### Summary of the optimizations
> **Default:**
![Default](./figures/ram1.png)

> **Hold `@FIL`**
![Stash @FIL](./figures/ram2.png)

> **Add register for `@COL`** to avoid waiting for the next `@COL`
![Stash @COL](./figures/ram3.png)

> **Add Counter** to omit later `@COL` requests when accessing sequential data (Just add the `@COL`-Offset)
![Timings](./figures/ram4.png)

### Lookups 
#### `Same bank, same page`
One `ACT` for `@Fila`, one `RD` for `@First Column`, second `@Second Column` for consecutive read. `PRE`.

#### Same page, different bank
Standard loading of the first block `ACT / @F`, `RD / @C`, `Data`, `PRE`. But, since we use two banks, we can launch the other (full) `ACT` / `READ` aswell. Lastly, we precharge the respective banks.
> **Note:** we have to continousily get data, therefore, the second `RD` can wait for the correct cycle.

#### Same bank, different page
Totally sequential
Act1 -> Rd1 -> data -> pre1 -> Act2 ...


### RAM Formulas
### Cycle time
$$
T_{\text{c}} = \frac{1}{GHz \times 10^9}
$$

Where:
- $T_{\text{c}}$ : Time for one cycle (s)
- $MHz$ : Frequency in GHz

### Theoretical Bandwith
$$
B_{\text{t}} = \frac{S_\text{Block}} {Cylces_{data}} \times GHz \times 10^9
$$

Where:
- $B_{\text{t}}$ : Theoretical time in B/s
- $Cycles_{data}$ : devoted for data readings
- $S_\text{Block}$ : Size of the read block in bytes
- ($\times 10^-9$ for GB/s)

**### Real Bandwith
$$
B_{\text{t}} = \frac{S_\text{Block}} {Cylces_{total}} \times GHz \times 10^9
$$

Where:
- $B_{\text{t}}$ : Theoretical time in B/s
- $Cycles_{total}$ : Cycles until precharge finished
- $S_\text{Block}$ : Size of the read block in bytes
- ($\times 10^-9$ for GB/s)**

### Wattage
$$
W = Cycles \times mA \times V
$$

Where:
- $W$ : Power (in watts)
- $mA$ : Amount of Cycles ($\times 10^-1$)
- $Cycles_{total}$ : Amount of Cycles 
- $V$ : Voltage

### Energy

$$
E = W \times t
$$
Where:
- $E$ : Energy in Joul
- $W$ : Wattage
- $t$ : Time in seconds 
- $V$ : Voltage

### Memory MTTF (Mbit) (per hour)
$$
MTTF_{Mbit} = \frac{10^9 hours}{Errors}
$$

### MTTF Mbit to bit
$$
MTTF_{bit} = MTTF_{Mbit} \times 10^6
$$

## Storage
### Calculating secotor transfer time
$$
T_{\text{transfer}} = \frac{Sectors \times Size_{sector}}{Bandwith \times 10^x}
$$

Where:
- $T_{\text{transfer}}$ : Time for transfer in seconds
- $Size_{sector}$ : Sector size in bytes
- $Bandwith \times 10^x$ : Bandwith in correct unit (e.g. $10^6$ if MB)


### Bandwith of
$$
Bandwidth = \frac{Amount of Data }{TransferredTime}
$$

Where:
- $Bandwidth$ : is typically measured in bits per second (bps), kilobits per second (Kbps), megabits per second (Mbps), or gigabits per second (Gbps), depending on the context.
- $Amount of Data Transferred$ : is measured in bits or bytes.
- $Time Taken$ : is measured in seconds.

### Effective Bandwith
$$
\text{Effective Bandwidth} = \frac{\text{TSize of Data Block}}{\text{Time Taken to Read the Data Block}}
$$

### RAID

RAID (Redundant Array of Independent Disks) is a data storage virtualization technology that combines multiple physical disk drive components into one or more logical units. 


### RAID Quick Summary
| RAID Level | Description                         | Pros                                 | Cons                                  | Bandwidth Impact                   |
|------------|-------------------------------------|--------------------------------------|---------------------------------------|------------------------------------|
| RAID 0     | Data striping without redundancy    | High performance                     | No redundancy, data loss risk         | Linear increase with more drives   |
| RAID 1     | Mirroring without striping or parity| Excellent redundancy, good read speed| High cost, limited write speed       | Read improves, write constant      |
| RAID 5     | Striping with distributed parity    | Balance of performance and redundancy| Write penalty, slow rebuild          | Improved read, write impacted      |
| RAID 6     | Similar to RAID 5 with double parity| Survives two drive failures          | Higher write penalty, complex parity | Slightly reduced write speed       |
| RAID 10    | RAID 1 + RAID 0 combination         | Performance and redundancy           | High cost, needs minimum four disks  | Excellent, scales well with drives |

#### RAID 0 
- Data is `stripe`, meaning distributed across `N` disks
- Available size is `N`*`Size`
- Bandwith is increased

#### RAID 1 
- Data is mirrired
- Excelent availability 
- All data is duplicated (`N/2` * `Size` available)
> **Overhead:** RAID 1 introduces a mayor overhead for keeping the disks coherent
 
#### RAID 2
![RAID2 Schema](./figures/raid2.png)
- Redundancy through `Hamming Code`
- Distributes data with bit-level interleaving
- Reads / Write accesses the same sector of all disks in parallel.
- ECC (Error Correcting Code) like in DRAM.
- ECC Code: Interleaved across several disks at the bit level using the Hamming method.
- Capable of detecting and correcting a single disk failure or detecting two disk failures. This is unique, but also adds complexity
- Special: Access on the bit level (most others have larger sectors)
> **Note:** A considerable amount of space is dedicated to redundant information. Due to the bit-level ECC and the need for extra disks to store the ECC codes


#### RAID 3
![RAID3 Schema](./figures/raid3.png)
- Distributes data with byte-level interleaving
- Dedicates one drive to parity
- The disk's ECC (Error Checking and Correction) information is used to detect errors. Data recovery is achieved by calculating the exclusive OR (XOR) of the information recorded on the other disks.
- I/O operation accesses the same sector of all disks in parallel.
> **Note:** Its transaction performance is poor because all the disks in the set have to operate together. 
 
#### RAID 4
![RAID4 Schema](./figures/raid4.png)
- Similar to RAID 3 but with striping at the stripe level.
- Disks can be accessed individually
- Data can be read from one disk without needing to engage the entire array
- Uses a disk for parity
- All writes have to write to the parity drive
- In case of failure of any of the disk units, the information can be reconstructed in real-time by performing a logical XOR operation at the stripe level
> **Bottle neck:** Since all writes result in a write to the parity drive, it is the bottle neck of the system

![RAID4 BN Schema](./figures/raid4-bottleneck.png)

#### RAID 5
![RAID5Schema](./figures/raid5.png)
- Like RAID 4, but the difference is that parity blocks are distributed among all disks.
- Independent and parallel access to disks for read operations, which enhances performance and speed.
-  Write operation is more complex than a simple write due to the need to update parity information. It involves reading the old data and old parity, calculating the new parity, and then writing the new data and new parity, hence the 2 reads and 2 writes.
> **Removes Write Bottle Neck:** For sufficiant amounts of discs, it performs like RAID0

##### Bandwith for sequential read
$$
Bandwith_{\text{RAID5}} = N \times Bandwith_{\text{Disk}}
$$

Where:
- $Bandwith_{\text{RAID5}}$ : Bandwith of the RAID5 unit
- $N$ : Amount of Disks in this set
  
##### Bandwith for sequential writes
$$
Bandwith_{\text{RAID5}} = (N-1) \times Bandwith_{\text{Disk}}
$$
> **Note:** The respective amount of one disc is dedicated to parity.

##### Bandwith for random writes
Now we write to a random sector. A write in a RAID5 consists of two reads and two writes.
$$
Bandwith_{\text{RAID5}} = \frac{N}{4} \times Bandwith_{\text{Disk}}
$$
  
 
#### RAID 6
![RAID6 Schema](./figures/raid6.png)
- Like RAID 5 uses striping across disks. 
- The key difference is that RAID 6 adds an additional layer of redundancy. 
- Tolerate the failure of two disks simultaneously, providing a higher level of data protection compared to RAID 5.
- Few commercial examples.
- More costly than other RAID levels. Controllers that support this double parity are more complex and expensive.
- Parity:
  - P is the parity stripe as in RAID 5.
  - Q is the second level of redundancy based on Reed-Solomon codes.
> **Two layers:** The P stripe is similar to the parity used in RAID 5. The Q stripe is an additional level of redundancy, utilizing Reed-Solomon codes, a robust error-correction coding system, which enhances fault tolerance.
 
> **Two disks can fail:** RAID 6 allows the array to continue functioning even if two disks fail simultaneously. The data can be reconstructed using the remaining disks and the parity information

- Allocates the equivalent of two disks' worth of space for storing parity information. However, unlike dedicating specific disks for parity, RAID 6 distributes this parity data across all disks in the array.

![RAID6 Write Schema](./figures/raid6-write.png)
> **Writing:** A write always needs 3 reads and 3 writes

- Read from the old sector, parity and Q
- Write to the new sector, the parity and the result of the R-S to Q



### General Observations
- **Redundancy vs. Performance**: Higher redundancy usually reduces performance, particularly in write operations.
- **Scalability**: RAID 0 and RAID 10 scale effectively in bandwidth with additional drives, whereas RAID 5 and RAID 6 face diminishing returns due to parity overhead.

###  Reliability of different RAID configurations
The probability of a disk failure occurring over time $t$ can be described by the exponential distribution formula:
$$
p(t) = 1 - e^{-\lambda t}
$$
where:
- $p(t)$ is the probability of failure by time $t$,
- $\lambda$ is the failure rate, equal to $\frac{1}{\text{MTTF}}$,
- $t$ is the elapsed time,
- $\text{MTTF}$ is the Mean Time To Failure.

### RAID 0 
If on disk fails, we have an error.
$$
\text{MTTF}_{\text{RAID0}} = \frac{\text{MTTF}_{\text{disk}}}{N}
$$
- RAID 0 fails if any one of the drives fails

### RAID 1 (N = 2)
$$
\text{MTTF}_{\text{RAID1}} = \frac{\text{MTTF}_{\text{disk}}^2}{N \times (N - 1) \times \text{MTTR}}
$$
- RAID 1 remains operational with the failure of one disk. It fails only if the second disk fails before the first one is replaced and rebuilt, within the MTTR.


### RAID 5 
$$
\text{MTTF}_{\text{RAID5}} = \frac{\text{MTTF}_{\text{disk}}^2}{N \times (N - 1) \times \text{MTTR}}
$$
- RAID 5 can tolerate the failure of one disk. It fails if a second disk fails before the first failed disk is replaced and rebuilt, within the MTTR. 

### RAID 6
$$ 
\text{MTTF}_{\text{RAID6}} = \frac{\text{MTTF}_{\text{disk}}^3}{N \times (N - 1) \times (N - 2) \times \text{MTTR}^2}
$$
- RAID 6 can tolerate the failure of any two disks. It fails if a third disk fails before the first two failed disks are replaced and rebuilt, within the MTTR.

### Overview
| Category              | RAID Level    | Pros                                                      | Cons                                          | Commercial Products      |
|-----------------------|---------------|-----------------------------------------------------------|-----------------------------------------------|--------------------------|
| **Independent Access**|               |                                                           |                                               |                          |
|                       | **RAID 0**    | No overhead                                               | No protection                                 | Widely used              |
| **Mirror Structure**  |               |                                                           |                                               |                          |
|                       | **RAID 1**    | No need for parity; fast recovery; fast reads; faster writes than other RAIDs | Higher overhead                            | EMC, HP (Tandem), IBM    |
| **Parallel Access**   |               |                                                           |                                               |                          |
|                       | **RAID 2**    | No disk needs to fail to be diagnosed                      | log2 N overhead                              | Not used                 |
|                       | **RAID 3**    | Low overhead; high bandwidth for large reads/writes       | No support for small reads/writes            | Storage Concepts         |
|                       | **RAID 4**    | Low overhead; more bandwidth for small reads              | Parity disk is a bottleneck for writes       | Network systems          |
| **Independent Access**|               |                                                           |                                               |                          |
|                       | **RAID 5**    | Low overhead; more bandwidth for small reads/writes       | Small writes require 4 disk accesses         | Widely used              |
|                       | **RAID 6**    | Protection against failure on 2 disks                     | Small writes require 6 disk accesses; increases overhead | Network systems          |

### RAID Combinations
### RAID 01
![RAID01 Schema](./figures/raid01.png)
  - Mirrors two stripes (RAID 0 arrays).
  - Pro: Offers the same performance as RAID 0 and can survive disk failures as long as all failed disks are in different RAID 0 arrays.
  - Con : If two disks fail and they are both part of the same RAID 0 stripe, the entire stripe fails, and the data on that stripe is lost.

### RAID 10
![RAID10 Schema](./figures/raid10.png)
    - Stripes across mirrors (pairs of RAID 1 arrays).
    - Pro: High fault tolerance (can lose one disk in each mirrored pair) and maintains high performance with better write speeds than RAID 01.
    -Con: Requires at least four disks and is more expensive in terms of disk usage compared to RAID 5.

### RAID 51
![RAID51 Schema](./figures/raid51.png)
    - A mirror of two RAID 5 arrays, adding an extra level of redundancy to RAID 5.
    - Pro: High data protection with the ability to withstand multiple disk failures.
    Con: Very high redundancy cost (half the storage capacity is used for mirroring), and it may have slower write performance due to double parity calculations.
    
### RAID 15
![RAID15 Schema](./figures/raid15.png)
    - Mirroring several RAID 5 arrays, not a standard or commonly implemented RAID level.
    - Pro: Theoretical high fault tolerance with the benefits of RAID 5's distributed parity.
    - Con: Extremely high cost for the level of redundancy and potentially complicated configuration and management.

### RAID 50
![RAID50 Schema](./figures/raid50.png)
    - A stripe across multiple RAID 5 arrays, combining the advantages of RAID 5's parity with RAID 0's performance.
    - Pro: Improved performance and fault tolerance; can lose one disk in each RAID 5 set without data loss.
    - Con: Requires a minimum of six disks and the cost of the additional disks for parity.

### RAID 05
![RAID05 Schema](./figures/raid05.png)
  - A stripe of RAID 5 arrays, less common and generally not recommended.
  - Pro  High read/write performance if small reads/writes dominate.
  - Con If a disk fails, the entire RAID 0 array in the RAID 5 set is at risk, making it vulnerable during rebuilds.


## Instructions
### Stack-Based Architecture
1. **Arithmetic/Logical Operations**
   - `Types`: ADD, SUB, MUL, DIV, AND, OR, XOR, CMPge, CMPeq.
   - `Mechanism`: Perform operation on top two stack elements; top element is replaced with result, increment `TOP`.

2. **Memory Access**
   - `PUSH @`: Decrease `TOP`, then push value from `M[@]` to stack.
   - `POP @`: Pop top stack value into `M[@]`, then increment `TOP`.

3. **Jump Instructions**
   - `Conditional (Bcond $)`: If `stack[TOP]` is true, add displacement to `PC` and increment `TOP`.
   - `Unconditional (BR $)`: Add displacement to `PC` directly.

        Operation: M[@] = stack[top]; top = top + 1
#### Example
$$
R = C - \frac{(A-B)}{(C-D)}
$$
```C
push D 
push C
sub
push B
push A
sub
div
push C
sub
pop R
```
Stack:
```C
           A
C          B   A-B               C
D   C-D   C-D  C-D  A-B/C-D   A-B/C-D  C-(A-B/C-D)
```

### Accumulator-Based Architecture
1. **Arithmetic/Logical Operations**
   - `Types`: ADD, SUB, MUL, DIV, AND, OR, XOR, CMPge, CMPeq, etc.
   - `Mechanism`: Operations are performed using the accumulator and another operand (either from memory or immediate value). The result is stored in the accumulator.

2. **Memory Access**
   - `LOAD @`: Load the value from memory address `M[@]` into the accumulator.
   - `STORE @`: Store the value from the accumulator into the memory address `M[@]`.

3. **Jump Instructions**
   - `Conditional (Bcond $)`: Perform the jump if a certain condition involving the accumulator's value is met.
   - `Unconditional (BR $)`: Jump unconditionally to the address specified by the displacement.

#### Example
$$
D = \frac{A + B \times C}{A}
$$
```C
load B 
mul C 
add A
div A
store D
```

### Addressing Mode

#### Definition
- An algorithm for accessing instruction operands.

#### Components
- **Addressing Mode**: Specifies the algorithm for effective address calculation.
- **Values Set**: Can include:
  - Address
  - Register
  - Displacement
  - Immediate value

#### Design Criteria
1. **Full Address Space Access**: Ability to reach any memory location.
2. **Efficient Data Structure Access**: Ease of accessing various data structures.
3. **Subroutine Communication**: Simplifies data and control transfer between main program and subroutines.

### Addressing Modes

### Register Mode
- **Description**: Operand is in one of the processor's registers.
- **Pros**:
  - Fast access ($\uparrow$)
  - Few bits required ($\uparrow$)
- **Cons**:
  - Need instructions to move data with memory ($\downarrow$)
- **Example**: `movl %edx, %eax`

### Immediate Mode
- **Description**: Operand is within the instruction.
- **Useful for**: Working with constants.
- **Example**: `movl $34, %eax`

### Absolute (Direct) Mode
- **Description**: Operand's address is in the instruction.
- **Cons**:
  - Many bits needed to encode address ($\downarrow$)
- **Example**: `movl 1242451, %eax`


### Register Indirect Mode
- **Description**: Instruction encodes the register containing the operand's address.
- **Pros**:
  - Few bits ($\uparrow$)
  - Autoincrement/autodecrement for arrays, stacks, etc. ($\uparrow$)
- **Examples**:
  - `movl (%ebx), %eax`
  - Autoincrement: `MOVL R1, (R2)+`
  - Autodecrement: `MOVL R1, -(R2)`

### Base + Displacement Mode
- **Description**: Address calculated using a register and a displacement (±).
- **If zero displacement**: Equivalent to register indirect mode.
- **Cons**:
  - Address calculation ($\downarrow$)
- **Example**: `movl -24(%ebp), %eax`

### Indexed Mode
- **Description**: Effective address obtained by adding contents of two registers.
- **Pros**:
  - Few bits required ($\uparrow$)
  - Useful for accessing vectors ($\uparrow$)
- **Cons**:
  - Address calculation ($\downarrow$)
- **Example**: `movl (%ebx, %esi), %eax`

### Scaled Mode
- **Description**: Especially useful for accessing vectors.
- **Scaling depends on**: Instruction.
- **Cons**:
  - Address calculation ($\downarrow$)
- **Example**: `movl -44(%ebx, %esi, 4), %eax`

### Post-Indirection
- **Description**: The data obtained from previous modes is used as the address of the operand.
- **Example**: Base + displacement with post-indirection.
- **Specific Example**: `MOVL @32(SP),R3`

### Post-Scaling
- **Description**: In VAX11 architecture, it was possible to combine scaled mode (indexed in DIGITAL terminology) with any other mode.
- **Example**: `MOVL @32(SP)[R7],R3`

### CISC: Complex Instruction Set Computer
- **Features**:
  - Instructions with high semantic content.
  - Emphasis on interpretation (microcode).

### RISC: Reduced (complexity) Instruction Set Computer
- **Features**:
  - Instructions with low semantic content.
  - Emphasis on compilation.

### Objective
- Goal: `T = N · CPI · Tc`

### CISC vs RISC Comparison
| Feature | CISC | RISC |
| ------- | ---- | ---- |
| Instruction Complexity | Complex Instructions | Simple Instructions |
| Instruction Size | Variable Size | Fixed Size |
| Instruction Formats | Many, depending on operands | Few instruction formats |
| Operand Location | In register or memory <br> Example: `ADDL %eax,(%ebx)` <br> (M[ebx] ← M[ebx] + eax) | Always in registers <br> Example: `ADD Ri, Rj, Rk` <br> (Rk ← Ri + Rj) |
| Operand in Memory | Any operand of any instruction can be in memory | Special instructions for memory access: Load / Store |
| Number of Registers | Historically few registers | Large register bank (≥32) |
| Addressing Modes | Complex addressing modes | Simple addressing modes (Rb + displacement) |




## CISC (Complex Instruction Set Computer)

- **Design Philosophy**:
  - Used complex instructions to align Machine Language (LM) closer to High-Level Languages (LAN).
  - Memory was scarce and expensive, program length was a key evaluation metric for architectures.
  - Introduction of microprogramming moved functions from a series of LM instructions to microprograms, increasing code density, reducing memory traffic, and decreasing program size, thereby enhancing machine efficiency.
  - Assumption: Moving complex instructions to LM would simplify compiler tasks by bridging the semantic gap between LM and High-Level Languages (e.g., INDEX, CASE, CALLS in VAX 11/70).

- **Characteristics**:
  - Many complex addressing modes.
  - Variable-length instructions complicating fetch and decoding.
  - Micro-memory reached significant sizes (e.g., 480 KB in VAX 11/70), becoming a system bottleneck and prone to errors.
<img src="./figures/cisc_0.png" alt="CISC" width="200"/>


## RISC (Reduced Instruction Set Computer)

- **Development Insight**:
  - Practical studies showed that CISC processors were oversized; compilers weren't using CISC addressing modes and instructions efficiently.
  
- **Design Philosophy**:
  - Utilizes very simple instructions that can be optimized when generated by compilers.
  - Compilers generate code more easily and efficiently for these machines.
  - From the 1980s, processors began to outpace memory speeds.

- **Characteristics**:
  - Many general-purpose registers, allowing most operands, including subroutine parameters and local variables, to reside in registers.
  - Memory is accessed only with load and store operations.
  - Designed for pipelined execution, aiming for one instruction per cycle.
<img src="./figures/risc_0.png" alt="RISC" width="150"/> 


### Microprogramming

#### Overview
- **Purpose**: Simplifies the design of the Control Unit in CISC processors.
- **Concept**: Implements a vertical, layered view of a computer's architecture.

#### Basic Elements of a Processor
1. **Processing Unit**:
   - Components: ALUs (Arithmetic Logic Units), Registers, Combinational Elements, etc.
2. **Control Unit**:
   - Nature: Sequential System.

#### Types of Control Units
- **Wired Control Unit**: Directly controls the execution of instructions through hardware.
- **Microprogrammed Control Unit**: Uses a set of microinstructions stored in memory to control the execution of instructions.

![Layers](figures/microprog.png)

### Formulas
- **Leakage Power Formula**: 
  $$
  P_{\text{leakage}} = I_{\text{leak}} \times V
  $$
  Where $I_{\text{leak}}$ is the leakage current, and `V` is the supply voltage.

- **Switching Power Formula**: 
  $$
  P_{\text{switching}} = \alpha \times C \times V^2 \times f
  $$
  Where $\alpha$ is the activity factor (fraction of time the capacitor is charging), `C` is the capacitive load, `V` is the supply voltage, and `f` is the frequency of operation.

### Total Power Consumption
- **Total Power**: 
  $$
  P_{\text{total}} = P_{\text{leakage}} + P_{\text{switching}}
  $$

### Energy Consumption
- **Energy Consumption Formula**: 
  $$
  E = P_{\text{total}} \times t
  $$
  Where `E` is the energy consumed, $P_{\text{total}}$ is the total power, and `t` is the time duration of program execution.

### Microprogramming

- **Micro Memory Content**: The content of micro memory is the microprogram.
- **Microprogram Composition**: Composed of microinstructions, equivalent to the states of the sequential system defining the control unit.
- **Microinstruction Fields**:
  1. **Control**: Bits that directly govern the circuits of the Processing Unit (UP).
  2. **Dir (Direction)**: Address of the next microinstruction, if it's necessary to break the implicit sequencing of the microprogram.
  3. **Cond (Condition)**: Method to evaluate flags and IR bits to decide if the jump to 'dir' is effective.
- **Phases in Microprogram**: Identifies phases in the execution of a Machine Language instruction:
  - Fetch
  - Decoding
  - Detailed Execution
- **Role**: The microprogram serves as the interpreter of Machine Language.

### Example Microprogram of MS
| Step | Instruction          | Description       |
|------|----------------------|-------------------|
| 0    | `MAR = PC; PC = PC+1`| FETCH             |
| 1    | `RD`                 |                   |
| 2    | `IR = MBR`           |                   |
| 3    | `IF IR15==1 GOTO 13` | DECODE            |
| 4    | `IF IR14==1 GOTO 9`  |                   |
| 5    | `MAR = SP; SP = SP+1`| ADD               |
| 6    | `RD; MAR = SP`       |                   |
| 7    | `MBR = MBR + A`      |                   |
| 8    | `WR; GOTO 0`         |                   |
| 9    | `MAR = SP; SP = SP+1`| SUB               |
| 10   | `RD; MAR = SP`       |                   |
| 11   | `MBR = MBR – A`      |                   |
| 12   | `WR; GOTO 0`         |                   |
| 13   | `IF IR14==1 GOTO 18` |                   |
| 14   | `A = SIGN(IR)`       | PUSH              |
| 15   | `SP = SP-1`          |                   |
| 16   | `MAR = SP; MBR = A`  |                   |
| 17   | `WR; GOTO 0`         |                   |
| 18   | `MAR = SP; SP = SP+1`| BEQ               |
| 19   | `RD`                 |                   |
| 20   | `ALU = MBR; IF Z==0 GOTO 0` |           |
| 21   | `A = SIGN(IR)`       |                   |
| 22   | `PC = PC+A; GOTO 0`  |                   |

### Wired Control Unit vs Microprogrammed Control Unit

#### Wired Control Unit
- **States (X)**: `k = log2(X)`
- **Inputs**: `m` bits (IR + cond)
- **Outputs**: `n` bits (control of UP)
- **ROM1**: `k·2^(m+k)` bits for calculating the next state
- **ROM2**: `n·2^k` bits for obtaining control signals associated with each state.

#### Microprogrammed Control Unit
- **Microinstructions (X)**: `k = log2(X)`
- **Inputs**: `m` bits (IR + cond)
- **Outputs**: `n` bits (control of UP)
- **Cond**: `c` bits for selecting the next microinstruction.
- **Micro Memory**: `(n+k+c)·2^k` bits for obtaining control signals associated with each state.
- **Seq**: `2^c+m` bits for selecting the next microinstruction.

#### Example
- **States**: 1024 (`k = 10`)
- **Inputs**: 14 bits (`m = 14`)
- **Outputs**: 24 bits (`n = 24`)
- **Cond**: 8 conditions (`c = 3`)

#### Cost Comparison
##### Wired Control Unit
- **ROM1**: `10 · 2^24 = 167,772,160` bits
- **ROM2**: `24 · 2^10 = 24,576` bits

##### Microprogrammed Control Unit
- **Micro Memory**: `37 · 2^10 = 37,888` bits
- **Seq**: `2^17 = 131,072` bits


### Assembly Code Examples

1. **ADDL Instruction**
   - Assembly Code: `ADDL $17, 36(%EBX, %EDX, 4)`
   - Operations:
     ```
     R1 ← M[EBX + EDX*4 + 36]
     R2 ← R1 + 17
     M[EBX + EDX*4 + 36] ← R2
     ```

2. **CALL Instruction**
   - Assembly Code: `CALL $1`
   - Operations:
     ```
     ESP ← ESP - 4
     M[ESP] ← EIP
     EIP ← EIP + displacement ($1)
     ```

3. **PUSHL Instruction**
   - Assembly Code: `PUSHL 100(,%EBX,8)`
   - Operations:
     ```
     R1 ← M[EBX*8 + 100]
     ESP ← ESP - 4
     M[ESP] ← R1
     ```

4. **RET Instruction**
   - Assembly Code: `RET`
   - Operations:
     ```
     EIP ← M[ESP]
     ESP ← ESP + 4
     ```

### Compilation vs Interpretation
1. **Java Program**
   - The process starts with a Java program, referred to as 'Programa P' written in Java.
   - The source code written in Java is a high-level representation of the program's instructions and logic.

2. **Compilation**
   - The Java source code is compiled by a Java compiler.
   - This compilation process translates the high-level Java code into Java bytecode, which is an intermediate form more optimized for execution but still independent of hardware.

3. **Java Virtual Machine (JVM)**
   - The Java bytecode is then executed by the Java Virtual Machine (JVM), which is a software-based interpreter.
   - The JVM is platform-specific, and in this case, it's implemented on an x86 architecture (denoted as 'INTÉRPRETE en x86 (JVM)').

4. **Interpreter and Data**
   - The JVM interprets the Java bytecode while interacting with data, which is typically stored in some form of memory or data storage (illustrated as 'DATOS').
   - The interpretation process involves reading the bytecode instructions, managing memory, and performing the operations defined by the bytecode.

5. **CPU Execution**
   - Within the x86 CPU, the bytecode is further translated into micro-operations (uops) by a translator component (denoted as 'TRADUCTOR a uops').
   - These micro-operations are hardware-specific instructions that the processor's execution units can directly execute.

6. **Micro-operation Interpreter**
   - An internal interpreter within the CPU (denoted as 'INTÉRPRETE de uops') interprets these micro-operations.
   - It utilizes the CPU's resources, such as the register bank and memory ('Banco de Registros Memoria'), to execute the micro-operations.

7. **Result**
   - The execution of these micro-operations leads to the final result ('resultado') of the program, which is then outputted or used by the program.


![JVM](figures/jvm.png)

## Advanced topics
### Basic Techniques in Processor Design

#### Memorization
- **Cache Memory**
- **Translation Lookaside Buffer (TLB)**
- **Prediction via**

#### Concurrency
- **Pipelining**
  - Segmented Cache
  - Segmented Writes
  - SDRAM (Synchronous Dynamic Random-Access Memory)

- **Parallelism**
  - DDR (Double Data Rate) Banks
  - Multi-bank Cache
  - RAID (Redundant Array of Independent Disks)

### Summary of Pipeline Processing in CPUs

#### Overview
- **Pipeline Movement**: Instructions, including data and control signals, move through the pipeline stages in a CPU.
- **Stages**: Each stage (Fetch, Decode/Load, Arithmetic, Memory Access, Write Back) operates concurrently, processing different instructions.
- **Efficiency**: With the hardware for executing one instruction, five independent instructions are concurrently executed.

#### Pipeline Stages
- **Fetch**: Retrieves instruction from memory.
- **Decode/Load**: Decodes the instruction and loads operands.
- **Arithmetic**: Performs computation.
- **Memory Access**: Accesses data from memory if needed.
- **Write Back**: Writes the result back to the register file.

#### Pipeline Execution
- Instructions move through each stage in successive cycles, enhancing overall CPU throughput.

#### Hazards in Pipeline
- **Data Hazards**: Occur when instructions depend on the results of previous instructions.
- **Control Hazards**: Arise from the execution of jump and branch instructions.
- **Structural Hazards**: Happen when multiple instructions require the same hardware resource simultaneously.

#### Example
- A typical sequence in the pipeline involves different stages processing parts of multiple instructions simultaneously.
#### Data 
![Data risk](figures/datarisk.png)
> **Problem:** The instruction `I1` calculates `R1` and it is used in the instruction `I2`. `I1` writes to `R1` in cycle 5, but `I2` reads the register `R1` in cycle 3, resulting in `I2` reading an incorrect value.

![control risk](figures/controlrisk.png)
> **Problem:** The instruction `I1` evaluates the jump condition in cycle 3 (stage A). Until that cycle, we do not know whether the jump will be effective. If the jump is effective, it leads to the erroneous initiation of the execution of two instructions (`I2` and `I3`).

### Not All Instructions Have the Same Stages

- **Complex Operations**: For instance, multiplication.
- **Difficult to Segment Operations**: Like division.
- **Floating Point Arithmetic**.

#### Instructions with Variable Execution Time
- **Memory Access**: With cache hits or misses (across different levels).

#### Management of Interruptions and Exceptions

### SuperScalar Processors

#### Goal: CPI < 1
- **Multiple Functional Units**: Equipped with several units for parallel processing.
- **Multiple Instruction Execution**: Capable of initiating more than one instruction (or operation) per cycle.
- **Still a Segmented Processor**: Maintains the pipeline architecture.
- **Variable Execution Times**: Instructions can have different execution times.
- **General Purpose Processors**: Most of the current general-purpose processors are superscalar.

### Out-of-Order SuperScalar Processors
#### Goal: CPI < 1
- **Out-of-Order Execution**: Many superscalar processors allow for Out-of-Order (OoO) execution.
- **Instruction Fetching**: Instructions are read in order but can be executed out of order.
- **Operand Dependency**: Execution of instructions is blocked if their operands are not available.
- **Execution Initiation**: Instructions begin execution when their operands are available and the corresponding Functional Unit (F.U.) is free.
- **General Purpose Processors**: Most of the current general-purpose processors are superscalar with out-of-order execution.

### Example of Out-of-Order Execution in SuperScalar Processors

Imagine a sequence of three instructions to be executed by a superscalar processor:

1. **Instruction 1 (I1)**: `R3 ← R1 + R2`
   - Adds the contents of registers R1 and R2 and stores the result in R3.
   - Requires the values in R1 and R2 to be ready.

2. **Instruction 2 (I2)**: `R5 ← M[R4]`
   - Loads data from the memory address contained in R4 into R5.
   - Depends on the memory access, which might take longer.

3. **Instruction 3 (I3)**: `R7 ← R6 - R3`
   - Subtracts the value in R3 from R6 and stores the result in R7.
   - Needs the result of I1 to be completed.

#### Execution Scenario in OoO Processor:
- **Cycle 1**: I1, I2, and I3 are fetched.
- **Cycle 2**: 
  - I1 is ready for execution (operands available).
  - I2 is waiting for memory (delayed).
  - I3 cannot execute yet as it depends on the result of I1.

- **Cycle 3**: 
  - I1 executes and completes.
  - I2 is still waiting.
  - I3 now has its operand from I1 but is waiting for a free Functional Unit.

- **Cycle 4**:
  - I2 is still waiting for memory.
  - I3 executes since its operands are ready and a Functional Unit is available.

- **Cycle 5**:
  - I2 finally accesses memory and executes.

#### Summary OoO:
- **Out-of-Order Execution**: I3, which was fetched after I2, is executed before I2 because its operands are ready and a functional unit is available.
- **Efficiency**: This OoO execution improves efficiency by not idly waiting for I2 to complete before starting I3.

### VLIW (Very Long Instruction Word)

#### Overview
- **Definition**: VLIW architectures feature a very large instruction size.
- **Objective**: To exploit Instruction Level Parallelism (ILP) aiming for CPI (Cycles Per Instruction) less than 1.

#### Characteristics
- **Multiple Independent Operations**: A single instruction specifies multiple independent operations.
- **Dedicated Functional Units**: Each operation is executed in a predetermined functional unit.
- **Static Instruction Scheduling**: Performed by the compiler rather than the processor.
- **Simplified Architecture Benefits**:
  - Higher frequency.
  - Lower power consumption.
  - Reduced cost.
  - More space for resources like registers, functional units (UFs), caches, etc.
  - Easier verification.

#### Processor Design
- **Segmented Processor**: Maintains a pipeline architecture.
- **Usage**: A significant percentage of manufactured processors are embedded, many of which are VLIW.

#### Example of VLIW Architecture
Consider a VLIW processor with a single instruction that contains four operations: two arithmetic operations, one memory load, and one memory store. The instruction might look something like this:

- **Instruction**: `[Add R1, R2; Sub R3, R4; Load R5, Addr; Store R6, Addr]`

In a traditional processor, these operations might be executed in separate instructions, possibly over four cycles. But in a VLIW processor, all these operations are packed into one instruction and can be executed in a single cycle, assuming no dependencies or resource conflicts. The compiler would have pre-determined that these operations do not interfere with each other and can be executed simultaneously.

#### Consideration
- **Compiler Dependency**: The efficiency of a VLIW processor heavily relies on the compiler's ability to effectively schedule instructions. Poor compiler optimization can lead to underutilization of the processor's capabilities.


### Overview
![Overview](figures/pipelines.png)

### Other formulas
#### Normalizing 
Where `P1` has the phases  $0.18\times  T +  0.48 \times T + 0.34 \times T = T$, if we parallelize `P2b` on 16 cores
$$
T_\text{Speedup1} = \frac{1}{0.18\times  T +  \frac{0.48 \times T }{16} + 0.34 \times T} = \frac{20}{11}
$$

$$
New Phases = \frac{0.18\times  T +  0.03 \times T  + 0.34 \times T}{\frac{20}{11}}
$$

We can normalize this by dividing by the speed up: 
$$
0.327\times  T +  0.054 \times T  + 0.618 \times T
$$



| Prefix | Power of 2 (Binary) | Power of 10 (Decimal) |
| ------ | ------------------- | --------------------- |
| Bit    | $2^0 (1)             | 10^0 (1)              |
| Kilo   | 2^10 (1,024)        | 10^3 (1,000)          |
| Mega   | 2^20 (1,048,576)    | 10^6 (1,000,000)      |
| Giga   | 2^30 (1,073,741,824)| 10^9 (1,000,000,000)  |
| Peta   | 2^50 (1,125,899,906,842,624) | 10^15 (1,000,000,000,000,000) |


# Vocabulary

| Spanish | English | German |
|---------|---------|--------|
| Rendimiento (m) | Performance | Leistung |
| Fiabilidad (f) | Reliability | Zuverlässigkeit |
| Tamaño (m) | Size | Größe |
| Ancho de banda (m) | Bandwidth | Bandbreite |
| Fuente (f) | Source/Power Supply | Quelle/Stromversorgung |
| Arquitectura (f) | Architecture | Architektur |
| Procesador (m) | Processor | Prozessor |
| Memoria (f) | Memory | Speicher |
| Almacenamiento (m) | Storage | Speicherplatz |
| Disco duro (m) | Hard drive | Festplatte |
| Entrada (f) | Input | Eingabe |
| Salida (f) | Output | Ausgabe |
| Red (f) | Network | Netzwerk |
| Sistema operativo (m) | Operating system | Betriebssystem |
| Caché (m) | Cache | Cache |
| Núcleo (m) | Core | Kern |
| Paralelismo (m) | Parallelism | Parallelität |
| Búfer (m) | Buffer | Puffer |
| Binario (m) | Binary | Binär |
| Base de datos (f) | Database | Datenbank |
| direccionamiento (m) | Addressing | Adressieren |
| Instrucciones de Secuenciamiento | Sequencing Instructions | Sequenzanweisungen |
| Salto | Jump | Sprung |
| Sumar | Add | Addieren |
| Desplazamiento | Shift | Verschieben |
| Llamada | Call | Aufruf |
| Bandera | Flag | Flagge |
| Puntero | Pointer | Zeiger |
| Estructura de Datos | Data Structure | Datenstruktur |
| Fila | Row | Reihe |
| Columna | Column | Spalte |
| Cara | Layer (or face) | Schicht (oder Gesicht) |
| Señal | Signal | Signal |
