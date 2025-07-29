<!--
SPDX-FileCopyrightText: 2017-2024 The PyPSA-Eur Authors
SPDX-License-Identifier: CC-BY-4.0
-->

[![zenodo PyPSA-Eur-PC](https://zenodo.org/badge/1021494699.svg)](https://doi.org/10.5281/zenodo.16566440)

# PyPSA-Eur-PC: PyPSA with added Photocatalysis (PC) Module

This repository is a fork of the main branch of the [PyPSA-Eur repository](https://github.com/pypsa/pypsa-eur) (branching of at v0.12.0) with the aim to introduce the new technology of photocatalysis to the original model.
The customized version PyPSA-Eur-PC is on the branch with the name pypsa-pc (default branch). The main project of PyPSA-Eur is in the main branch of this repository to maintain the history of the project.

For the operation with this model [atlite-pc](https://github.com/w-tusche/atlite-pc.git) is required, a custom version of [atlite](https://github.com/pypsa/atlite) where photocatalysis is added. See usage for the installation.

For documentation of the main PyPSA-Eur project and atlite please refer to the official documentation.

- [Docs PyPSA-EUR](https://pypsa-eur.readthedocs.io/en/latest/)
- [Docs atlite](https://atlite.readthedocs.io/en/latest/)

## Contributions

The model extension in this fork was done with contributions from:

- Wolfram Tuschewitzki
- Jelto Lange
- Leander Raudszus

Related content to PyPSA-Eur-PC:

- [atlite-pc](https://github.com/w-tusche/atlite-pc.git)
- Analysis and plotting code for paper "Impacts of photocatalytic hydrogen production on the European energy system": [photocatalysis-europe](https://github.com/w-tusche/photocatalysis-europe.git)
- [Raw data of PC-0 and PC-50 cases for paper: Impacts of photocatalytic hydrogen production on the European energy system](https://10.5281/zenodo.16360844)

## Usage

To use this software go through the following steps:

```bash
git clone https://github.com/w-tusche/pypsa-eur
cd pypsa-eur
```

The package requirements are curated in the envs/environment.fixed.linux.yaml file. Thus install the required packages using [mamba](https://mamba.readthedocs.io/en/latest/index.html):

```bash
mamba update conda

mamba env create -f envs/environment.fixed.linux.yaml  # on other platforms try it with the environment.yaml file

mamba activate pypsa-pc
```

For running PyPSA-Eur-PC the custom [atlite-pc](https://github.com/w-tusche/atlite-pc.git) is required. For this we download it and install it inside the `pypsa-eur` folder and install it in development mode:

```bash
# make sure the current directory is pypsa-eur
git clone https://github.com/w-tusche/atlite-pc.git

cd atlite-pc

conda activate pypsa-pc
# Install local atlite module for development (make sure correct branch is checked out)
python -m pip install -e . 

cd ..
```

Now everything should be set up. To run the model we supply an example config file and custom cost file that should be placed in resources (careful, if you purge with snakemake it will be deleted.)

Config file: `config\config.elec_s_150_lv1.25__I-H_2045.yaml`
Custom cost file (costs and efficiency PC): `resources\costs_2040.csv`

Now you can do a first run:

```bash
snakemake -call all --configfile config/config.elec_s_150_lv1.25__I-H_2045.yaml
```

Photocatalysis costs and efficiency have to be changed in the custom cost file.

It might be that renaming the root folder from pypsa-eur-pc to `pypsa-eur` might fix runtime errors.

Post-processing steps for the resulting data can be found in the following repository: Analysis and plotting code for paper "Impacts of photocatalytic hydrogen production on the European energy system": [photocatalysis-europe](https://github.com/w-tusche/photocatalysis-europe.git)

## Licence

The code in PyPSA-Eur and also PyPSA-Eur-PC is released as free software under the
[MIT License](https://opensource.org/licenses/MIT), see [`doc/licenses.rst`](doc/licenses.rst).
However, different licenses and terms of use may apply to the various
input data.
