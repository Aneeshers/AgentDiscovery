# PACE: Adaptive Parameter-free Optimization ⚡️
[![arXiv](https://img.shields.io/badge/arXiv-2405.16642-b31b1b.svg)](https://arxiv.org/abs/2405.16642) [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1c5OxMa5fiSVnl5w6J7flrjNUteUkp6BV?usp=sharing)

This repository is the official implementation of the **PACE** optimizer in ***Pick up the PACE: A Parameter-Free Optimizer for Lifelong Reinforcement Learning***.

How can you _quickly_ adapt to new tasks or distribution shifts? Without knowing when or how much to adapt? And without _ANY_ tuning? 
 🤔💭

Well, we suggest you go fast. 🏎️💨 Go ahead and pick up (the) **PACE**.

**PACE** is a parameter-free optimizer for continual environments inspired by [online convex optimization](https://arxiv.org/abs/1912.13213) and uses [discounted adaptive online prediction](https://arxiv.org/abs/2402.02720).

## Implement with only one line change.
Like other [meta-tuners](https://openreview.net/pdf?id=uhKtQMn21D), PACE can work with any of your continual, fine-tuning, or lifelong experiments with just one line change.

```python
from pace import start_pace
# original optimizer
optimizer = torch.optim.Adam
lr = 0.001
optimizer = start_pace(log_file='logs/pace.text', optimizer)(model.parameters(), lr=lr)
```

After this modification, you can continue using your optimizer methods exactly as you did before. Whether it's calling `optimizer.step()` to update your model's parameters or `optimizer.zero_grad()` to clear gradients, everything stays the same. PACE seamlessly integrates into your existing workflow without any additional overhead.

## Control Experiments

We recommend running ``main.ipynb`` in Google Colab. This approach requires no setup, making it easy to get started with our control experiments. If you run locally, to install the necessary dependencies, simply:

```setup
pip install -r requirements.txt
```
![Control Experiment](figures/control.png)


## Vision-based RL Experiments

Our vision-based experiments are hosted in the `vision_exp` directory, which is based off [this Procgen Pytorch implementation](https://github.com/joonleesky/train-procgen-pytorch). These experiments allow exploration of different gaming environments using the **PACE** optimizer for adaptive learning.

To initiate an experiment with the default configuration in the Procgen "starpilot" environment, use the command below. You can easily switch to other game environments, like Atari, by altering the `--exp_name="Atari"` parameter:

```bash
python vision_exp/train.py --exp_name="procgen" --env_name="starpilot" --optimizer="pace" --warmstart_step=0
```
<p align="center">
  <img src="figures/games1.gif" alt="Game 1" width="30%">
  <img src="figures/games2.gif" alt="Game 2" width="30%">
  <img src="figures/games3.gif" alt="Game 3" width="30%">
</p>
