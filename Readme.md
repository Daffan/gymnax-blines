# Training & Speed Evaluation Tools for [`gymnax`](https://github.com/RobertTLange/gymnax)

<a href="https://github.com/RobertTLange/gymnax-blines/blob/main/docs/logo.png?raw=true"><img src="https://github.com/RobertTLange/gymnax-blines/blob/main/docs/logo.png?raw=true" width="215" align="right" /></a>


In this repository we provide training pipelines for [`gymnax`](https://github.com/RobertTLange/gymnax) agents in JAX. Furthermore, you can use the utilities to speed benchmark step transitions.

## Accelerated Training of Agents with [`gymnax`](https://github.com/RobertTLange/gymnax)

We provide training routines and the corresponding checkpoints for both Evolution Strategies (mostly OpenES using [`gymnax`](https://github.com/RobertTLange/evosax)) and PPO. You can train the agents as follows: 

```
python train.py -config configs/<env_name>/ppo.yaml
python train.py -config configs/<env_name>/es.yaml
```

## Visualize [`gymnax`](https://github.com/RobertTLange/gymnax) Environment Rollouts

You can also generate GIF visualizations of the agent's behaviour as follows:

```
python visualize.py -env <env_name>
```

Note that we do not support visualizations for most behavior suite environments, since they do not lend themselves to visual display (e.g. markov reward process, etc.).

|  |  |  |  | 
| --- | --- | --- | --- |
| ![](docs/Pendulum-v1.gif) | ![](docs/Acrobot-v1.gif)  | ![](docs/CartPole-v1.gif) | ![](docs/MountainCarContinuous-v0.gif) |
| ![](docs/Catch-bsuite.gif) | ![](docs/FourRooms-misc.gif)  | ![](docs/MetaMaze-misc.gif) | ![](docs/PointRobot-misc.gif) |

## Speed Up Evaluations for [`gymnax`](https://github.com/RobertTLange/gymnax)

Finally, we provide simple tools for benchmarking the speed of step transitions on different hardware (CPU, GPU, TPU). For a specific environment the speed estimates can be obtained as follows:

```
python speed.py -env <env_name>
```

## Running Grid Search with the `MLE-Infrastructure`

```
pip install mle-toolbox
mle run ...
```

## MinAtar Comparison with Torch DQN

In order to make sure that we fully replicate the world dynamics of the NumPy based MinAtar API, we provide different checks:

- Transition test assertions from random and trained behaviour.
- Performance test from DQN agents trained on the NumPy environment in the JAX environment.
- Performance test from DQN agents trained on the JAX environment in the NumPy environment.

We first replicate train the DQN agents using the code provided in the MinAtar repository without any parameter tuning. E.g.

```
cd examples
python dqn.py -g breakout -v -s
```