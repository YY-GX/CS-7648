# Safe-and-Sample-efficient-Reinforcement-Learning-for-Clustered-Dynamic-Uncertain-Environments

## Table of Contents
- [Introduction](#Introduction)
- [Install](#install)
- [Usage](#usage)

## Introduction
We provide code for evaluate the safety and sample-efficiency of our proposed RL framework.

For safety, we use Safe Set Algorithm (SSA).   
For efficiency, there are more strategies you can choose:  
1, Adapting SSA;  
2, Exploration (PSN, RND, None);  
3, Learning from SSA;  

The safety and efficiency results of all models are shown below
![safety_result](docs/safety_result.png)
![efficiency_result](docs/efficiency_result.png)

We also provide visual tools.
![visulization](docs/visualization.png)


## Install

```
conda create -n safe-rl
conda install python=3.7.9
pip install tensorflow
pip install keras
pip install matplotlib
pip install gym
pip install cvxopt
```

or

```
conda create -n safe-rl python=3.7.9 -y
conda activate safe-rl
pip install -r requirements.txt
```

## Usage

```
# Train regular RL
python train.py --display {none, pyglet} --explore {none, psn, rnd} --no-qp --mode rl
python train.py --display {none, pyglet} --explore {none, psn, rnd} --qp --mode rl

> python train.py --display none --explore none --no-qp --mode rl

# Train RL with safe controller
python train.py --display {none, pyglet} --explore {none, psn, rnd} --no-qp --mode safe

> python train.py --display none --explore none --no-qp --mode safe

# Human Intervention Training (First time)
python train.py --display pyglet --explore none --no-qp --mode human

# Human Intervention Training (From Second time, Load buffer / If you want to continue your training) 
python train.py --display pyglet --explore none --no-qp --mode human --isHumanBuffer True

# Run RL with human buffer
python train.py --display pyglet --explore none --no-qp --mode rl --isHumanBuffer True
> python train.py --display none --explore none --no-qp --mode rl --isHumanBuffer True

# Load model
# For example1, load 100 eps rl default:
python train.py --display none --explore none --no-qp --mode rl --isLoadModel True --loadModelCheckpointPth ./model_checkpoints/rl/default/1


python train.py --display none --explore none --no-qp --mode safe --isLoadModel True --loadModelCheckpointPth ./model_checkpoints/safe/circle/5 --env circle


python train.py --display none --explore none --no-qp --mode rl --isHumanBuffer True --isLoadModel True --loadModelCheckpointPth ./model_checkpoints/human/cross/5 --env cross

# For example2, load 100 eps baseline2 default:
python train_baseline2.py --display none --isLoadModel True --loadModelCheckpointPth ./model_checkpoints/baseline2/default/1
```
- `--display` can be either `none` or `pyglet` (visulization).
- `--explore` specifies the exploration strategy that the robot uses. 
- `--no-qp` means that we use vanilla SSA.
- `--qp` means that we use adapted SSA.
<!-- - `--no-ssa-buffer` means that we use the default learning.
- `--ssa-buffer` means that we use the safe learning from SSA demonstrations. -->
- `--mode` means that we use which approach: rl/safe/human
- `--isHumanBuffer` means that use saved human buffer or not.
- `--env` means the training env we use, if not specified, we use default env. To use other envs, choose either `cross` or `circle`.

