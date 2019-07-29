# SESC: SuperESCalar Simulator
I am not a project member of SESC. This is a clone with some of my tweaks. Original unmodified source code can be found at http://sesc.sourceforge.net/.


SESC is a CPU state simulator.

Key takeways for me:
* Files in `src/confs` contain configurations for running simulations, including number of cores, cache size, block size, set associativity, etc.
* This simulator uses a simple bus architecture. See files in `src/libmem/` and `src/libcmp/SMPSystemBus`
* The cache coherence protocol used is (D)MESI, which is a distributed invalidate-based protocol commonly used for write-back caches. It's distributed across cores, where each cache slice serves a set of blocks. Instead of read/write requests going to the bus, they're sent via network to a directory entry.
* There are two types of coherence misses. ***True sharing***: different cores access the same data. ***False sharing***: different cores access different data but in the same block. False sharing was ignored in this case.
