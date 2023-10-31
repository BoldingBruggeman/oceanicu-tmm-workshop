# OceanICU Transport Matrix Method (TMM) workshop

*This page may be still edited until the time of the workshop in response to participant feedback.*
At present (31 October) these instructions have been confirmed to work on at least some Windows, Linux and Mac systems.

The purpose of the workshop is be able to operate the TMM implementation developed within [OceanICU](https://ocean-icu.eu/).
It will be possible to use a variety of biogeochemical models, including [MOPS](https://doi.org/10.5194/gmd-8-2929-2015), [ERSEM](http://ersem.com), [PISCES](https://www.pisces-community.org/).
While we will visualize selected results, this workshop is not aimed at in-depth result evaluation or validation.

The aim is that all participants will be able to run a TMM simulation on "private" hardware - i.e. a personal laptop/workstation or HPC-system.
To make this possible, a few tasks will have to be done by each participant before the workshop starts.

We will work in a terminal window while installing necessary files and running TMM. This looks different on different platforms:
* On Windows, use the "Anaconda prompt" from the start menu (instructions on how to install that below).

We will be editing Pyhton scripts files with model configurations. This can be done with many different editors, e.g., [Visual Studio Code](https://code.visualstudio.com/), Notepad on Windows, `vi` on Linux/Mac. We recommend using one you are already familiar with.

## 1. Install TMM software

This does *not* require administrator or root permissions.

1. Ensure you have Anaconda:
   - Linux/Mac: execute `conda --version` in a terminal
   - Windows: look for “Anaconda prompt” in the start menu

   If you *do not* have Anaconda, install Miniconda on [Linux](https://conda.io/projects/conda/en/stable/user-guide/install/linux.html), [Windows](https://conda.io/projects/conda/en/stable/user-guide/install/windows.html), or [Mac](https://conda.io/projects/conda/en/stable/user-guide/install/macos.html).

2. Create an isolated `fabmos` environment with the model and visualization tools:
    ```
    conda create -n fabmos -c bolding-bruggeman -c conda-forge fabmos oceanicu
    ```
    If you experience any issue with the above, we recommend you first execute `conda update conda` to ensure your conda is up to date.
    Should this fail because of lack of permissions, we recommend you install Miniconda as described under the previous option. After
    you have an up-to-date conda, retry the `conda create ...` command.

## 2. Install TMM configurations

A number of different TMM configurations have been made available by Samar Khatiwala [here](http://kelvin.earth.ox.ac.uk/spk/Research/TMM/TransportMatrixConfigs/). For this workshop we suggest to use the MITgcm_2.8deg configuration. Download and un-tar the configuration and record the path to folder as it will be used later.



## 3. Install FABM configurations and TMM run-scripts

The installed version of FABM-OS contains a number of biogeochemical models. This [zip file](https://raw.githubusercontent.com/BoldingBruggeman/oceanicu-tmm-workshop/main/tmm_workshop.zip) contains the necessary FABM configuration files and FABM-OS (TMM) run-scripts. 

Please download and unzip the file and record where it has been un-zipped.

**If the above has succeeded, you are ready for the workshop.
Instructions below are for reference during and after the workshop only.**

## 4. Running TMM

Every time you open a terminal window, activate the `fabmos` environment:
```
conda activate fabmos
```
Change folder to where the TMM configuration was un-packed - e.g.:
```
cd /data/kb/OceanICU/MITgcm_2.8deg
```
 
The TMM code is prepared for parallel operation - i.e. utilize a number of cores available on the computer system. This is achieved by using the Message Passing Interface (MPI) standard. Operating MPI enabled programs has a slight different syntax as shown in the example below:

```
mpiexec -n 10 python ~/OceanICU/TMM-workshop/examples/tmm/MOPS.py
```
    
This will run the TMM configuration from the Python script MOPS.py on 10 processes in parallel.

The TMM implementation uses domain decomposition to split the workload between the available resources.

When the program finishes a NetCDF formatted output file have been created and can be viewed by a number of different visualization tools - e.g. pyncview - that should be available as part of the installation done in 1.2.
