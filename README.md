## Quick Start
##### Use the QuickStart.ipynb notebook for a quick start.
In the notebook, you can find the minimal implementation for generating sample-wise unlearnable examples on CIFAR-10.
Please remove `mlconfig` from `models/__init__.py` if you are only using the notebook and copy-paste the model to the notebook.



## Experiments in the paper.
Check scripts folder for *.sh for each corresponding experiments.

## Sample-wise noise for unlearnable example on CIFAR-10
##### Generate noise for unlearnable examples
```console
python3 perturbation.py --config_path             configs/cifar10                \
                        --exp_name                path/to/your/experiment/folder \
                        --version                 resnet18                       \
                        --train_data_type         CIFAR10                       \
                        --noise_shape             50000 3 32 32                  \
                        --epsilon                 8                              \
                        --num_steps               20                             \
                        --step_size               0.8                            \
                        --attack_type             min-min                        \
                        --perturb_type            samplewise                      \
                        --universal_stop_error    0.01
```
##### Train on unlearnable examples and eval on clean test
```console
python3 -u main.py    --version                 resnet18                       \
                      --exp_name                path/to/your/experiment/folder \
                      --config_path             configs/cifar10                \
                      --train_data_type         PoisonCIFAR10                  \
                      --poison_rate             1.0                            \
                      --perturb_type            samplewise                      \
                      --perturb_tensor_filepath path/to/your/experiment/folder/perturbation.pt \
                      --train
```


## Class-wise noise for unlearnable example on CIFAR-10
##### Generate noise for unlearnable examples
```console
python3 perturbation.py --config_path             configs/cifar10                \
                        --exp_name                path/to/your/experiment/folder \
                        --version                 resnet18                       \
                        --train_data_type         CIFAR10                       \
                        --noise_shape             10 3 32 32                     \
                        --epsilon                 8                              \
                        --num_steps               1                              \
                        --step_size               0.8                            \
                        --attack_type             min-min                        \
                        --perturb_type            classwise                      \
                        --universal_train_target  'train_subset'                 \
                        --universal_stop_error    0.1                            \
                        --use_subset
```
##### Train on unlearnable examples and eval on clean test
```console
python3 -u main.py    --version                 resnet18                       \
                      --exp_name                path/to/your/experiment/folder \
                      --config_path             configs/cifar10                \
                      --train_data_type         PoisonCIFAR10                  \
                      --poison_rate             1.0                            \
                      --perturb_type            classwise                      \
                      --perturb_tensor_filepath path/to/your/experiment/folder/perturbation.pt \
                      --train
```


---
