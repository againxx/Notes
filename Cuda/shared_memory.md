# Shared Memory

## Bank Conflict
* To achieve high memory bandwidth, shared memory is divided into 32 equally-sized memory modules, called _banks_, which can be accessed simultaneously
* When multiple addresses in a shared memory request fall into the same bank, a _bank conflict_ occurs, the hardware splits a request into as many seprate conflict-free transactions as necessary

Three typical situations occur when a request to shared memory is issued by a warp:
* **Parallel access**: multiple addresses accessed across multiple banks
* **Serial access**: multiple addresses accessed within the same bank (the worst case)
* **Broadcast access**: a single address read in a single bank

* Serial access is the worst pattern: When multiple addresses fall into the same bank, the request must be serialized
* A bank conflict does not occur when two threads from the same warp access the same address
    - for read accesses, the word is broadcast to the requesting threads
    - for write accesses, the word is written by only one of the threads - which thread performs the write is undefined

## Access Mode
* Shared memory bank width defines which shared memory addresses are in which shared memory banks. Memory bank width varies for devices depending on compute capability
* Neighboring words are classified in different banks to maximize the nubmer of possible concurrent accesses for a warp
* There are two different bank widths:
    - 4 bytes (32-bits) for devices of compute capability 2.x
    - 8 bytes (64-bits) for devices of compute capability 3.x

For 32-bits bank width, the mapping from shared memory address to bank index can be calculated as follows
```
bank index = (byte address / 4 bytes/bank) % 32 banks
```

For 64-bit mode, successive 64-bit words map to successive banks
* A shared memory request from a warp **does not** generate a bank conflict if two threads access any **sub-word** within the same 64-bit word
* As a result, 64-bit mode always causes the same or fewer bank conflicts for the same access pattern on Kepler devices relative to Fermi

### Configuration
The default access mode can be queried using the API function `cudaDeviceGetSharedMemConfig(cudaSharedMemConfig *pConfig)` (this function seems only useful in Kepler architecture)

### Compute Capability 5.x
* Shared memory has 32 banks that are organized such that **successive** 32-bit words map to **successive** banks
* Each bank has a bandwidth of 32 bits per clock cycle
