# Pulsar Timing Environments

This repository offers a centeralized location for the IPTA Pulsar Timing & Data Combination Teams' environment.

## Installation of the Conda Environments

Please note, we highly encourage using a fresh install of [Mambaforge](https://github.com/conda-forge/miniforge#mambaforge) over a default install of Anaconda/Miniconda. If you must use an Anaconda/Miniconda installation, from a fresh environment install the [Mamba Environment & Package Handler](https://github.com/mamba-org/mamba) via `conda install -c conda-forge mamba`.

To install this environment in your flavor of Anaconda, proceed through the following steps:
  1. Clone this directory: `git clone https://github.com/ipta/pulsar-env.git`
  2. Enter the cloned directory: `cd pulsar-env`
  3. Using `mamba`, install the environment: `mamba env create -f anaconda-env.yml`
  4. Activate the environment: `mamba activate IPTA_Env`

### Important Note Regarding the Included OpenMPI
For Linux 64, Open MPI is built with CUDA awareness but this support is disabled by default. To enable it, please set the environment variable `OMPI_MCA_opal_cuda_support=true` before launching your MPI processes. Equivalently, you can set the MCA parameter in the command line: `mpiexec --mca opal_cuda_support 1 ...`
 
In addition, the UCX support is also built but disabled by default. To enable it, first install UCX (`conda install -c conda-forge ucx`). Then, set the environment variables `OMPI_MCA_pml="ucx"` and `OMPI_MCA_osc="ucx"` before launching your MPI processes. Equivalently, you can set the MCA parameters in the command line: `mpiexec --mca pml ucx --mca osc ucx ...`

Note that you might also need to set `UCX_MEMTYPE_CACHE=n` for CUDA awareness via UCX. Please consult UCX's documentation for detail.
