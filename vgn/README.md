# vgn

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Data Generation](#data-generation)
- [Training](#training)
- [Evaluation](#evaluation)

## Prerequisites

The package was tested on Ubuntu 18.04 and Python 3.6.
OpenMPI is used to distribute the data generation.

```
sudo apt install python3-dev python3-pip libopenmpi-dev
```

## Installation

Clone the repository into the `src` folder of a catkin workspace.

```
git clone https://github.com/ethz-asl/grasp_playground
```

Create and activate a new virtual environment.

```
cd grasp_playground
virtualenv -p python3 .venv
source .venv/bin/activate
```

Install the Python dependencies within the activated virtual environment.

```
pip install -r vgn/requirements.txt
```

## Data Generation

Collect a set of synthetic grasp attempts with

```
python scripts/generate_data.py --root path/to/dataset
```

Run `generate_data.py -h` to print the full list of arguments.
The data generation can also be distributed over multiple processors using MPI.

```
mpiexec -n <n-procs> python scripts/generate_data.py ...
```

## Training

Train a VGN model on the generated dataset using

```
python scripts/train_vgn.py --net conv --data-dir path/to/dataset --log-dir path/to/logdir
```