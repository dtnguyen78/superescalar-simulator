# superescalar-simulator
Clone of SESC (a microprocessor simulator) with some of my tweaks


Original unmodified source code can be found at http://sesc.sourceforge.net/


Key takeways:
* Files in `src/confs` contain configurations for running simulations, including number of cores, cache size, block size, set associativity, etc.
* This simulator uses a simple bus architecture. See files in `src/libmem/` and `src/libcmp/SMPSystemBus`
* The cache coherence protocol I used was directory-based MESI, which is a distributed invalidate-based protocol commonly used for write-back caches. It's distributed across cores, where each cache slice serves a set of blocks. Instead of read/write requests going on the bus, they're sent via the network to a directory entry.
* There are two types of coherence misses. ''True sharing:'' different cores access the same data. ''False sharing:'' different cores access different data but in the same block. I ignored false sharing in my code modifications.
