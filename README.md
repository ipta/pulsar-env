![Conda Env Test](https://github.com/IPTA/pulsar-env/actions/workflows/test_CondaEnv.yml/badge.svg)
![Apptainer Build (Ubuntu)](https://github.com/IPTA/pulsar-env/actions/workflows/test_Singularity.yml/badge.svg)

# Pulsar Timing Environments

This repository offers a centeralized location for the IPTA Pulsar Timing & Data Combination Teams' environment.

Currently, this repository presents the following:
- An Anaconda Environment for Pulsar Science (`anaconda_env.yml`)
- Singularity/Apptainer Container for HPC Resources (`containers/Singularity`)

## Installation of the Conda Environment

Please note, we highly encourage using a fresh install of [Mambaforge](https://github.com/conda-forge/miniforge#mambaforge) or [MicroMamba](https://mamba.readthedocs.io/en/latest/user_guide/micromamba.html)over a default install of Anaconda/Miniconda. If you must use an Anaconda/Miniconda installation, from a fresh environment install the [Mamba Environment & Package Handler](https://github.com/mamba-org/mamba) via `conda install -c conda-forge mamba`.

**Note:** As of `conda` version 22.11, `libmamba` can be used as a solver to speed up basic Anaconda installs (though there are growing pains). You can find out more [at the official posting](https://www.anaconda.com/blog/a-faster-conda-for-a-growing-community).

To install this environment in your flavor of Anaconda, proceed through the following steps:
  1. Clone this directory: `git clone https://github.com/ipta/pulsar-env.git`
  2. Enter the cloned directory: `cd pulsar-env`
  3. Using `mamba`, install the environment: `mamba env create -f anaconda-env.yml`
  4. Activate the environment: `mamba activate IPTA_Env`

### Important Note Regarding the Included OpenMPI
For Linux 64, Open MPI is built with CUDA awareness but this support is disabled by default. To enable it, please set the environment variable `OMPI_MCA_opal_cuda_support=true` before launching your MPI processes. Equivalently, you can set the MCA parameter in the command line: `mpiexec --mca opal_cuda_support 1 ...`
 
In addition, the UCX support is also built but disabled by default. To enable it, first install UCX (`conda install -c conda-forge ucx`). Then, set the environment variables `OMPI_MCA_pml="ucx"` and `OMPI_MCA_osc="ucx"` before launching your MPI processes. Equivalently, you can set the MCA parameters in the command line: `mpiexec --mca pml ucx --mca osc ucx ...`

Note that you might also need to set `UCX_MEMTYPE_CACHE=n` for CUDA awareness via UCX. Please consult UCX's documentation for detail.

## Docker
Docker is a program which builds interactive virtual machines (containers) that are designed to be somewhat integrated with the host machine. They are easily deployed on many different hardware infrastructures, but are often not allowed on High Performace Computing (HPC) machines due to the security risk it poses ([read more](https://linuxconcept.com/getting-privileged-access-inside-a-docker-container-your-guide-to-enhanced-control/)). However, it is exceedingly useful for JupyterHub instances or quick roll-out during workshops.

### To Build the Container:
To build the Docker image, follow the latest instructions for the `docker build` command found [here](https://docs.docker.com/reference/cli/docker/image/build).

## Apptainer/Singularity

Apptainer (former name: Singularity) is a program to build virtual machines (containers) with desired OS and programs. These can be easily deployed and ran on other computers. 
Containers are build based on the recipies called "definition files", here we provide a definition file `Singularity`. Note, sometimes definition files have an extension `.def`, which we also refer to in the instructions below.

The current definition file contains `tempo2`, `enterprise`, and other primary packages for IPTA DR3 data analyses.

### To Build the Container:
To build the Apptainer image (`IPTA-Env.sif`), you need to first have Apptainer installed on your machine as well as administrator access. If you plan to use this image on an HPC resource, you should contact your HPC administrator to build the image for you to ensure proper linkage with the desired MPI libraries and relevant compilers. Once installed, a system adminstrator can build the container via:

```
sudo apptainer build IPTA-Env.sif containers/Singularity.def
```

### To Browse the Container:
Once installed and the image is built, any user of that local machine can access the Apptainer image via a shell instance by running:
```
apptainer shell --bind "/virtual_home_directory/:$HOME"  IPTA-Env.sif`
```
Where `/virtual_home_directory/` is the path to your home directory on your local machine. 

### For Building Containers Inside Windows WSL via Ubuntu

In Windows Store, there is [Ubuntu app](https://apps.microsoft.com/detail/9pdxgncfsczv?hl=en-US&gl=US) that allows to run the popular Linux OS as a command-line shell in Windows. However, by default, it is based on Windows Subsystems for Linux v1 (WSL1). Make sure to upgrade from WSL1 to WSL2. You can read more about this procedure via the [official guide from Microsoft](https://learn.microsoft.com/en-us/windows/wsl/install). This requires also may requre updating settings in BIOS.

To be able to use graphical interface (PGPLOT) in tempo2 plk plugin, a proper display redirection is required:
1. From within the **Windows command-line**, obtain the local IPv4 address for the machine: `ipconfig`.
2. Open the Ubuntu app.
3. Edit the `$HOME/.bash_profile` file found in **Ubuntu** to have the following line at the end: `export DISPLAY=172.26.32.1:0.0`
4. Close the Ubuntu app. 
5. Install [Xming](https://sourceforge.net/projects/xming/) for Windows, which creates an XServer instance on the Windows OS.
6. Run Xming with `-ac` argument via XLaunch. 
7. Finally, open the Ubuntu app and run your commands as normal. The graphical interfaces should appear as expected via an Xmimg instance.

