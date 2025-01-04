# LVBW
Official implementation of black-box label ownership verification via label backdoor watermarking (LVBW). Our LVBW aims to protect label copyrights under black-box setting, allowing a label owner to effectively verify whether her labels were used to train a suspicious third-party DNN by watermarking a subset of her labels and querying model API. Our codes is based on [https://github.com/SewoongLab/FLIP].

---
## Abstract
TODO
---

## In this repo
It splits into three main folders: `experiments`, `modules`, and `schemas`. The `experiments` folder contains subfolders and `.toml` configuration files on which an experiment may be run. The `modules` folder stores source code for each of the subsequent part of an experiment. These modules take in specific inputs and outputs as defined by their subseqeunt `.toml` documentation in the `schemas` folder. Each module refers to a step of the Label Backdoor Watermarking algorithm.

### Existing modules:
1. `base_utils`: Utility module, used by the base modules.
1. `train_expert`: Step 1 of watermarking: training expert models and recording trajectories.
1. `generate_labels`: Step 2 of watermarking: generating poisoned labels from trajectories.
1. `select_flips`: Step 3 of watermarking: strategically flipping labels within some budget. 
1. `train_user`: Use watermarked labels to train a model. Evaluate watermarking by ACC/ASR of this model and get verification results（i.e.,p-value and △P）.

More documentation can be found in the `schemas` folder.

### Supported Datasets:
1. CIFAR-10
1. CIFAR-100
1. Tiny ImageNet
---
## Installation:
conda env create -f environment.yml
conda activate LVBW

### Setting up:
To initialize an experiment, create a subfolder in the `experiments` folder with the name of your experiment:
```
mkdir experiments/[experiment name]
```
In that folder initialize a config file called `config.toml`. An example can be seen here: `experiments/example_attack/config.toml`.

The `.toml` file should contain references to the modules that you would like to run with each relevant field as defined by its documentation in `schemas/[module name]`. 

### Running a module:
At the moment, all experiments must be manually run using:
```
python run_experiment.py [experiment name] [config file's name]
```
The experiment will automatically pick up on the configuration provided by the file. 

As an example, to run the `example_attack` experiment one could run:
```
python run_experiment.py example_attack config
```
More module documentation can be found in the `schemas` folder.
