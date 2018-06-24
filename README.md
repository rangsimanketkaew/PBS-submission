# PBS-submission
Automated script for interactive PBS job submission. <br />
These scripts can be only used for PBS Professional on TAIWANIA cluster. <br />
Source code customization is required for other Job Scheduler and other cluster.

### Gaussian 16
* [subg16](subg16) 
* Usage: `subg16 inputfile` <br />
where input is your g16 input file with or without .com extension. For instance,  <br />
`subg16 water_hf` <br />
`subg16 water_hf water_hf_4cores.`
* If no output specified, basename of input will be used to name output file automatically.

* This G16 runtime supports only OpenMP (shared-memory) parallel method.  <br />
  This program recognizes the OMP threads from the value of %nproc line in input.  <br />
  Max %nprocs is 40 and sensible value of %nproc are: 1, 2, 4, 8, 12, 16, 24, 32, and 36.

* Warning: If %nproc is set to 1, G16 job will be submitted in serial queue.  <br />
           If %nproc is 2 through 40, G16 job will be submitted in cf40 queue instead.
* For requesting of other queue, we suggest you to modify the PBS script of cf40 as your need.


### Q-Chem
* subqchem
* Usage: `subqchem inputfile` <br />
where input file is Q-Chem input with or without .in extension.
* Details: Parallelizability of Q-Chem that run in parallel with shared-memory (MPI) is better than that of non-shared memory (OpenMP).
* This script supports the Q-Chem PBS job submission only with OpenMP method. If you want to use MPI instead, talk to TAIWANIA staff.

### NWChem 
* [subnwchem](subnwchem)
* Usage: `subnwchem [gpu||casper||mpipr] [help]`
* EXAMPLE: subnwchem gpu                submit NWChem using CUDA  <br />
           subnwchem gpu casper      submit NWChem using CUDA and Casper

* IT can be used to submit NWChem job with and without using ARMCI methods, Casper and MPI-PR, and with and without GPU/CUDA. Note that GPU/MPI-PR is not available.

* COMMANDS

| argument | Task |
| :---: | --- |
| gpu      | Requests GPU accelerator | 
| casper   | Requests Casper method (against MPI-PR) |
| mpipr    | Requests MPI-PR method (against Casper) | 
| help     | Open this help |

* LIMITATION

| Quantity | Maximum value |
| --- | --- |
| Compute node | 600 |
| CPU cores | 40 (per node) |
| MPI process | 40 (per node) |
| Threads | 40 (per node & per MPI process) |

* CONTACT                 Rangsiman Ketkaew  rangsiman1993@gmail.com

* MORE DETAILS            NWChem Official Website  [http://www.nwchem-sw.org](http://www.nwchem-sw.org)  <br />
                         NWChem Official manual   [https://github.com/nwchemgit/nwchem/wiki](https://github.com/nwchemgit/nwchem/wiki)
                         
### Multiple NWChem jobs
* subnwmult
* Usage: subnwmult input.1.nw [ input.2.nw | input.3.nw | ... ]
* READ BEFORE USE: 
1. Basename of input file will be used for naming output file. E.g. nwchem.nw => nwchem.out
2. Existing files whose basename is similar to name of submitting input will be replaced.
3. Neither ARMCI Casper, nor MPIPR, and nor GPU/CUDA are supported now.

---

### How to download and activate
1. Open Githup source code of script.
2. Click on "Raw"
3. Copy URL address
4. Open your Linux terminal then use the following command for downloading the script.
```
wget the/url/address/of/raw/source/code
```
5. Activate script using the following command
```
chmod +x script.file
```

Rangsiman Ketkaew
rangsiman1993@gmail.com

