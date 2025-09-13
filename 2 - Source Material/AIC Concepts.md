**Pipelining** is an “assembly-line” technique where instruction execution is split into stages so multiple instructions progress simultaneously—one per stage each clock cycle. It boosts **throughput** (instructions finished per unit time) rather than the latency of a single instruction.

Typical 5 stages: **IF** (fetch) → **ID** (decode/register read) → **EX** (execute) → **MEM** (memory) → **WB** (write-back).

Key points:

* Speedup is limited by the slowest stage and by pipeline fill/flush time.
* Hazards reduce efficiency: **structural** (resource conflicts), **data** (e.g., RAW), and **control** (branches).
* Mitigations: **stalls/bubbles**, **forwarding**, **branch prediction/speculation**, and wider/out-of-order pipelines.

A **superscalar processor** is a CPU that can start (issue) **multiple instructions in the same clock cycle** by using several parallel execution units (e.g., multiple ALUs, FP units). Goal: raise **IPC** (instructions per cycle) beyond 1.

How it works (at a glance):

* **Wide fetch/decode**: read and decode several instructions each cycle.
* **Multiple pipelines/units**: run independent ops in parallel.
* **Register renaming**: remove false deps (WAR/WAW).
* **Dynamic scheduling / out-of-order exec**: pick ready instructions; **reorder buffer** retires them in program order.
* **Branch prediction**: keeps the machine fed.

Contrast with **pipelining**: pipelining overlaps stages of many instructions but typically starts **one** per cycle; superscalar tries to start **several** per cycle.

Limits: available **instruction-level parallelism**, true data deps (RAW), cache misses/memory bandwidth, and branch mispredictions. Example: a “4-wide” core can begin up to 4 independent instructions each cycle—if the code and resources allow it.

**Feature size** is the size of a transistor. If the feature size decreases, the density of the transistor increases (number of transistors)