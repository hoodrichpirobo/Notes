
| Theory (T)              | Seminar (S)                     | Lab Practice (P)                    |
| ----------------------- | ------------------------------- | ----------------------------------- |
| **T0: **                | —                               | —                                   |
| **T1: Introduction**    | **S1: Introduction**            | —                                   |
| **T2: Shared memory**   | **S2: Programming with OpenMP** | **P1: Parallelization with OpenMP** |
| **T3: Message passing** | **S3: Programming with MPI**    | **P2: Parallelization with MPI**    |
Supercomputing is a synonym of parallel computing or high performance computing.

OpenMP is for shared memory, and MPI is for distributed memory.

Exatflop is $10^{18}$
Back then, the technology kept improving through increasing the clock frequency, now it increases through increasing the cores/threads.
The difference between shared memory and distributed memory is that  the first one shares the memory and the other has each CPU with their respective memory which other can access.
There can also be a hybrid model, where they are distributed but on each node they have a multiprocessor that shares memory
OpenMP is based on directives, that is, their parallel programming methodology chosen is semi-automatic parallelization (compiler directives).
MPI is based on libraries, that is, their parallel programming methodology chosen is libraries of subroutines or functions (API)