# Apptainer/Singularity

Apptainer (former name: Singularity) is a program to build virtual machines (containers) with desired OS and programs. These can be easily deployed and ran on other computers. 
Containers are build based on the recipies called "definition files", here we provide a definition file `Singularity`. Note, sometimes definition files have an extension `.def`, which we also refer to in the instructions below.

The current definition file contains `tempo2`, `enterprise`, and other primary packages for IPTA DR3 data analyses.

## To build a container:

`sudo apptainer build new_sif_file_name.sif def_file.def`

## To browse container content:

`apptainer shell --bind "/virtual_home_directory/:$HOME"  pulsarenv_official_20240220.sif`

Where `/virtual_home_directory/` is a path on your local machine 

## For building containers inside Windows WSL Ubuntu (Ubuntu for Windows)

In Windows Store, there is Ubuntu app that allows to run Ubuntu shell in Windows. However, by default, it is based on WSL1. Make sure to upgrade from WSL1 to WSL2. This requires also updating settings in BIOS.

To be able to use graphical interface (PGPLOT) in tempo2 plk plugin, a proper display redirection is required:

1. In .bashrc in Ubuntu, `export DISPLAY=172.26.32.1:0.0`, where the IP address (v4) can be obtained in Windows command line prompt by running `ipconfig`.
2. Install Xming for Windows.
3. Run Xming with `-ac` argument via XLaunch. Then open Ubuntu.
