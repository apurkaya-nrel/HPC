## AMR-Wind on Kestrel

AMR-Wind is a massively parallel, block-structured adaptive-mesh,
incompressible flow solver for wind turbine and wind farm
simulations. The primary applications for AMR-Wind are: performing
large-eddy simulations (LES) of atmospheric boundary layer (ABL)
flows, simulating wind farm turbine-wake interactions using actuator
disk or actuator line models for turbines, and as a background solver
when coupled with a near-body solver (e.g., Nalu-Wind) with overset
methodology to perform blade-resolved simulations of multiple wind
turbines within a wind farm. For more information see
https://github.com/Exawind/amr-wind

NREL makes available modules for using Amr-Wind, while users are free
to build there own versions if they so choose. It is recommended that
AMR-Wind be run on GPU nodes for obtaining the most optimal
performance, so these modules are built for running on GPU nodes for
different toolchains.

Here is a sample script for submitting an AMR-Wind application run on multiple GPU nodes, with the users input file, mesh grid and solver.

??? example "Sample job script: Kestrel - Full GPU node"

    ```

    #!/bin/bash
    #SBATCH --time=1:00:00 
    #SBATCH --partition=gpu-h100
    #SBATCH --account=<user-account>
    #SBATCH --nodes=2
    #SBATCH --gres=gpu:h100:4
    #SBATCH --exclusive

    module restore 
    source /nopt/nrel/apps/gpu_stack/env_cpe23.sh
    module load PrgEnv-nvhpc

    srun -K1 -n 16 --gpus-per-node=4 ../amr_wind abl_godunov-512.i >& ablGodunov-512.log

    ```

