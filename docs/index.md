# ddp-batch

This repository offers specialized scripts designed to facilitate the execution of **_ab initio_ random structure searching ([AIRSS](https://www.mtg.msm.cam.ac.uk/Codes/AIRSS))** package and **ephemeral data derived potential ([EDDP](https://www.mtg.msm.cam.ac.uk/Codes/EDDP))** packages. These scripts are tailored for use with batch queuing systems or job schedulers, specifically the **SLURM** (Simple Linux Utility for Resource Management) and **SGE** (Sun Grid Engine), on cluster and high-performance computing (HPC) environments. The provided scripts streamline the process of initializing, managing, and monitoring AIRSS and EDDP tasks, ensuring efficient utilization of the cluster/HPC resources.

## Installation
install the package with:

`git clone git@github.com:sehunjoo/ddp-batch.git`

run setup.sh script:

`./setup.sh`

## Documentation

### update-chain

- This script is for generating `chain-batch` script, which is a `chain` script for batch queueing system. It basically replaces `spawn` and `despawn` with `spawn-batch` and `despawn-batch`.
- Usage

  Generate the chain-batch with:
 
  `./update-chain`

### spawn-batch

- This script can be used to submit multiple jobs to a cluster using a batch queueing system. This script is for creating a job script, submitting the job script, monitoring the job, and resubimtting/killing the job.
- This script is applicable to all applications, but is specifically designed for use with `airss.pl` and `crud.pl` in  AIRSS package and `forge` in EDDP package.
- It creates `jobscript-program.sh` and `despawn-batch` files in the working directory. As soon as a job is started, a `.spawnpid.*` file is created for each subjob. The file contains details of each subjob.
- It automatically resubmits the job if the job is terminated due to the wall clock limit.
- For example,

  `nohup spawn-batch -command airss.pl -mpinp 4 -seed Li -max 100 &`

- The following command line can be used to stop the spawn-batch script and the running jobs. The `spawn-batch` script detects the STOP file, runs `despawn-batch` and stops itself.

  `touch STOP`

### farm-batch

- This script is exactly same as `spawn-batch` script. This script is merely a counterpart to the `farm` script that is included in the EDDP package.


## References
- [Pickard, Ephemeral data derived potentials for random structure search, 2022.](https://doi.org/10.1103/PhysRevB.106.014102)
- [Salzbrenner et al., Developments and further applications of ephemeral data derived potentials, 2023.](https://doi.org/10.1063/5.0158710)
