# Project 3. MIPS Pipelined Simulator
Skeleton developed by CMU,
modified for KAIST CS311 purpose by THKIM, BKKIM and SHJEON.

## Instructions
There are three files you may modify: `util.h`, `run.h`, and `run.c`.

### 1. util.h

We have setup the basic CPU\_State that is sufficient to implement the project.
However, you may decide to add more variables, and modify/remove any misleading variables.

### 2. run.h

You may add any additional functions that will be called by your implementation of `process_instruction()`.
In fact, we encourage you to split your implementation of `process_instruction()` into many other helping functions.
You may decide to have functions for each stages of the pipeline.
Function(s) to handle flushes (adding bubbles into the pipeline), etc.

### 3. run.c

**Implement** the following function:

    void process_instruction()

The `process_instruction()` function is used by the `cycle()` function to simulate a `cycle` of the pipelined simulator.
Each `cycle()` the pipeline will advance to the next instruction (if there are no stalls/hazards, etc.).
Your internal register, memory, and pipeline register state should be updated according to the instruction
that is being executed at each stage.

### CPU_State (`util.h`)

#### Latch-register group `<latch>_NOOP`

Flag to indicate whether instruction at the corresponding stage should be ignored. Used when flushing and stalling.

#### Latch-register group `<latch>_II`

Contains _instruction index_ for `INST_INFO`.

#### Latch-register group `<latch>_NPC`

Contains `PC`+4 where `PC` is value of `CURRENT_STATE.PC` at the time corresponding instruction was fetched. Used to reset `CURRENT_STATE.PC` when flushing.

#### Latch-register group `<latch>_DEST`

Either contains 99 if the corresponding instruction doesn't write-back, or contains the register number it writes-back to.

#### Latch-registers for `ID_EX`

* `ID_EX_REG1` - value of `rs` register if instruction has `rs` field
* `ID_EX_REG2` - value of `rt` register if instruction has `rt` field
* `ID_EX_IMM` - value of the immediate if instruction has `imm` field
* `ID_EX_RS` - value of `rs` field if instruction has one
* `ID_EX_RT` - value of `rt` field if instruction has one

#### Latch-registers for `EX_MEM`

* `EX_MEM_ALU_OUT` - output of the ALU
* `EX_MEM_WRITE_VAL` - value of `rt` register (used for `sw` instruction)

#### Latch-registers for `MEM_WB`

* `MEM_WB_VAL` - the value to be written to register `MEM_WB_DEST`
