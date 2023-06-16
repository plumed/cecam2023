# CECAM 2023 - software

In this repository we report a brief guide on how to install the software needed for CECAM 2023 workshop.
Our recommendation is to use conda. Unfortunately we can only provide precompiled conda packages for x64 architecture, Linux and MacOS.
This means that if you want to run the exercise on a different architecture (e.g., a new Mac with a ARM processor) you should install the software on your own.

First, make sure conda is installed by typing:
```
conda
```
If the command is not found, please refer to these [instructions to install conda on your machine](https://docs.conda.io/en/latest/miniconda.html).
Alternatively, if you use the [Homebrew package manager](https://brew.sh/), you can install conda with:
```
brew install --cask anaconda
# add this line to your .bashrc
export PATH="/usr/local/anaconda3/bin:$PATH"
```

Now we can create a conda environment for the PLUMED Masterclass:
```
conda create --name plumed-cecam-2023
```

and activate it with:
```
conda activate plumed-cecam-2023
```

Finally, we can proceed with the installation of the required software:
```
# install some basic analysis tool and the default plumed version
conda install -c conda-forge plumed py-plumed numpy pandas matplotlib notebook jupyterlab mdtraj mdanalysis git
```
If the exercise requires Gromacs, you can then run the following command:
```
# install plumed 2.9.0 and gromacs 2020.7 with MPI and all modules enabled
conda install --strict-channel-priority -c plumed/label/cecam-2023 -c conda-forge plumed gromacs
```
If the exercise requires LAMMPS instead, the appropriate command is:
```
# install plumed 2.9.0 and lammps 23 Jun 2022 with MPI and all modules enabled
conda install --strict-channel-priority -c plumed/label/cecam-2023 -c conda-forge plumed lammps
```
If the exercise requires AMBER, you should first create a separate AMBER environment:
```
# create a separate AMBER environment and install AMBER
conda create --name plumed-cecam-2023-amber
conda activate plumed-cecam-2023-amber
conda install -c conda-forge ambertools
```
And you should then stack the PLUMED and AMBER environments:
```
# stack the PLUMED and AMBER environments
conda activate plumed-cecam-2023
conda activate --stack plumed-cecam-2023-amber
export PLUMED_KERNEL=/your_path_here/plumed-cecam-2023/lib/libplumedKernel.so
```

Conda will install a number of packages.
On MacOS, for instance, when installing plumed 2.9.0 and gromacs 2020.7 with MPI and all modules enabled, you should see something similar to this:
```
The following NEW packages will be INSTALLED:

  boost-cpp          conda-forge/osx-64::boost-cpp-1.82.0-hd754db5_1
  gromacs            plumed/label/cecam-2023/osx-64::gromacs-2020.7-h75233e6_1
  libhwloc           conda-forge/osx-64::libhwloc-1.11.13-hcf6850d_2
  mpi                conda-forge/osx-64::mpi-1.0-openmpi
  openmpi            conda-forge/osx-64::openmpi-4.1.5-h4fe9131_101

The following packages will be SUPERSEDED by a higher-priority channel:

  plumed             conda-forge::plumed-2.9.0-nompi_he44c~ --> plumed/label/cecam-2023::plumed-2.9.0-h75233e6_0

```
 Make sure that `gromacs` and `plumed` packages are installed from `plumed/label/cecam-2023`.
 
 **Do not forget to activate the plumed-cecam-2023 environment every time you open a new terminal/shell.**
 
 Notice that with some outdated conda version you might receive an error due to the fact that conda confuses python 3.1 with python 3.10.
 If you find an error like this one:
 ```
 PackagesNotFoundError: The following packages are not available from current channels:

  - python=3.1

 ```
 Make sure that you have at least conda 4.11.0 (or update conda with `conda update conda`).
 More at [this link](https://github.com/conda/conda/issues/11065)

