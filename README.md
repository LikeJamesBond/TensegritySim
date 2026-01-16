# Tensegrity Sim

This repo contains code to create a simulation for tensegrity structures. It allows for continuous cables and 2D, 2.5D and 3D structures. 

## Research Context

Tensegrity Sim is a Python-based simulation framework developed to support research on tensegrity mechanisms, with an emphasis on continuous cable models and mixed-dimensional (2D, 2.5D, and 3D) structures.  

The software is designed to support reproducible simulation of static equilibrium configurations under prescribed control inputs, and to facilitate extension toward optimization, control, and hardware-in-the-loop experimentation.

This repository accompanies the paper:

> TensegritySim Python Package Using Virtual Work, submitted to the ASME Journal of Mechanisms and Robotics.

All simulations presented in the paper can be reproduced using the configuration files provided in the `yaml` directory.

## Reproducibility and Usage

To get started with development, clone the repo and install the dependencies.

I reccommend using a venv to keep the libraries for this project separate from the main python interpreter. To create a venv, from the project's main directory run `python3 -m venv ./venv`. Now everytime you want to use this venv run `source venv/bin/activate`. To deactivate simply use the `deactivate` command. 

This project uses Python3, in order to run it you will need some dependencies. To get them you can run `pip install -r requirements.txt` (with the venv active)

To run the project:
```bash
python3 main.py <path/to/yaml/config>
```
Sample yaml config files are provided in the `yaml` directory. To understand how to change the simulation to your needs, see the [simulation setup](docs/setup.md) documentation. 

## Installation

If instead of helping develop the project you want to use it as a library, you can install it using pip. To install the project, to use as a library, run `pip install .` from the project's main directory. This will install the `TensegritySim` module and allow you to import it in your own projects.

If you want to install from a different directory, you can run `pip install <path/to/project>` or `pip install -e <path/to/project>` to install in editable mode. Or without cloning the repo, you can run `pip install git+<git-repo-url>`.

## Definitions and Conventions (as used in this project)
Strings - Strings are connection types that only carry tension, they lengthen as force is applied  
Bar - A bar can carry either tension or compression, but does not change length  
Forces - Tensions are positive values and compression forces in connections are negative.

## Modeling Assumptions

The simulation framework adopts the following modeling conventions:

- Strings carry tension only and may change length under load.
- Bars may carry tension or compression and are assumed to be inextensible.
- Tension forces are represented as positive values; compression forces are negative.
- Equilibrium configurations are computed using numerical optimization.

These assumptions are consistent with those described in the accompanying paper.

## Organization
`main.py` provides an example entry point for running simulations using YAML-defined models and control inputs.

### TensegritySim Module
The `TensegritySim` directory contains all the code TensegritySim python module.
* `data_structures.py` contains the `Node`, `Connection`, `Control`, and `Tensegrity` classes
* `yaml_parser.py` reads the yaml file and returns the Tensegrity object. See [YAML Reference](docs/yaml.md) for how to format the yaml file
* `visualization.py` shows the tensegrity structure using matplotlib
* `tensegrity_solver.py` uses an optimizer to solve for an updated structure

### yaml
The `yaml` directory contains sample yaml files for running the sim
