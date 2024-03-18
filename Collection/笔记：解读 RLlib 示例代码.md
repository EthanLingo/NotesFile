---
title:
  - 笔记：解读 RLlib 示例代码
authors: Ethan Lin
year: 2024-03-18
tags:
  - 类型/AI问答笔记
  - 日期/2024-03-18
---
# 笔记：解读 RLlib 示例代码




> [!attention]
> 以下由AI回答，不保证正确性！




示例代码：

`rock_paper_scissors_dummies.py`：

```python
import gymnasium as gym
import numpy as np
import random
from ray.rllib.policy.policy import Policy
from ray.rllib.policy.view_requirement import ViewRequirement

ROCK = 0
PAPER = 1
SCISSORS = 2


class AlwaysSameHeuristic(Policy):
    """Pick a random move and stick with it for the entire episode."""

    def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)
        self.exploration = self._create_exploration()
        self.view_requirements.update(
            {
                "state_in_0": ViewRequirement(
                    "state_out_0",
                    shift=-1,
                    space=gym.spaces.Box(ROCK, SCISSORS, shape=(1,), dtype=np.int32),
                )
            }
        )

    def get_initial_state(self):
        return [random.choice([ROCK, PAPER, SCISSORS])]

    def is_recurrent(self) -> bool:
        return True

    def compute_actions(
        self,
        obs_batch,
        state_batches=None,
        prev_action_batch=None,
        prev_reward_batch=None,
        info_batch=None,
        episodes=None,
        **kwargs
    ):
        return [state_batches[0][0] for x in obs_batch], state_batches, {}


class BeatLastHeuristic(Policy):
    """Play the move that would beat the last move of the opponent."""

    def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)
        self.exploration = self._create_exploration()

    def compute_actions(
        self,
        obs_batch,
        state_batches=None,
        prev_action_batch=None,
        prev_reward_batch=None,
        info_batch=None,
        episodes=None,
        **kwargs
    ):
        def successor(x):
            # Make this also work w/o one-hot preprocessing.
            if isinstance(self.observation_space, gym.spaces.Discrete):
                if x == ROCK:
                    return PAPER
                elif x == PAPER:
                    return SCISSORS
                elif x == SCISSORS:
                    return ROCK
                else:
                    return random.choice([ROCK, PAPER, SCISSORS])
            # One-hot (auto-preprocessed) inputs.
            else:
                if x[ROCK] == 1:
                    return PAPER
                elif x[PAPER] == 1:
                    return SCISSORS
                elif x[SCISSORS] == 1:
                    return ROCK
                elif x[-1] == 1:
                    return random.choice([ROCK, PAPER, SCISSORS])

        return [successor(x) for x in obs_batch], [], {}

    def learn_on_batch(self, samples):
        pass

    def get_weights(self):
        pass

    def set_weights(self, weights):
        pass

```



> [!question]


解读代码
```python
class AlwaysSameHeuristic(Policy):
    """Pick a random move and stick with it for the entire episode."""

    def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)
        self.exploration = self._create_exploration()
        self.view_requirements.update(
            {
                "state_in_0": ViewRequirement(
                    "state_out_0",
                    shift=-1,
                    space=gym.spaces.Box(ROCK, SCISSORS, shape=(1,), dtype=np.int32),
                )
            }
        )
```

这个策略。这个方法形参是什么形状的数据？输出是什么？或者说，要得到一个什么结果？

> [!AI]

这个[`AlwaysSameHeuristic`](command:_github.copilot.openSymbolInFile?%5B%22venv%2Flib%2Fpython3.9%2Fsite-packages%2Fray%2Frllib%2Fexamples%2Fpolicy%2Frock_paper_scissors_dummies.py%22%2C%22AlwaysSameHeuristic%22%5D "venv/lib/python3.9/site-packages/ray/rllib/examples/policy/rock_paper_scissors_dummies.py")类是一个策略类，它继承自[`Policy`](command:_github.copilot.openSymbolInFile?%5B%22venv%2Flib%2Fpython3.9%2Fsite-packages%2Fray%2Frllib%2Fpolicy%2Fpolicy.py%22%2C%22Policy%22%5D "venv/lib/python3.9/site-packages/ray/rllib/policy/policy.py")类。在这个类中，[`__init__`](command:_github.copilot.openSymbolInFile?%5B%22venv%2Flib%2Fpython3.9%2Fsite-packages%2Fray%2Frllib%2Fexamples%2Fpolicy%2Frock_paper_scissors_dummies.py%22%2C%22__init__%22%5D "venv/lib/python3.9/site-packages/ray/rllib/examples/policy/rock_paper_scissors_dummies.py")方法是初始化方法，用于设置策略的初始状态。

在[`__init__`](command:_github.copilot.openSymbolInFile?%5B%22venv%2Flib%2Fpython3.9%2Fsite-packages%2Fray%2Frllib%2Fexamples%2Fpolicy%2Frock_paper_scissors_dummies.py%22%2C%22__init__%22%5D "venv/lib/python3.9/site-packages/ray/rllib/examples/policy/rock_paper_scissors_dummies.py")方法中，首先调用了父类的[`__init__`](command:_github.copilot.openSymbolInFile?%5B%22venv%2Flib%2Fpython3.9%2Fsite-packages%2Fray%2Frllib%2Fexamples%2Fpolicy%2Frock_paper_scissors_dummies.py%22%2C%22__init__%22%5D "venv/lib/python3.9/site-packages/ray/rllib/examples/policy/rock_paper_scissors_dummies.py")方法，然后创建了一个探索对象，最后更新了[`view_requirements`](command:_github.copilot.openSymbolInFile?%5B%22venv%2Flib%2Fpython3.9%2Fsite-packages%2Fray%2Frllib%2Fpolicy%2Fpolicy.py%22%2C%22view_requirements%22%5D "venv/lib/python3.9/site-packages/ray/rllib/policy/policy.py")字典。

[`view_requirements`](command:_github.copilot.openSymbolInFile?%5B%22venv%2Flib%2Fpython3.9%2Fsite-packages%2Fray%2Frllib%2Fpolicy%2Fpolicy.py%22%2C%22view_requirements%22%5D "venv/lib/python3.9/site-packages/ray/rllib/policy/policy.py")字典定义了策略需要的视图要求。在这个例子中，它需要一个名为`state_in_0`的视图，这个视图需要从`state_out_0`中获取数据，并且数据的形状是`(1,)`，数据类型是[`np.int32`](command:_github.copilot.openSymbolInFile?%5B%22venv%2Flib%2Fpython3.9%2Fsite-packages%2Fray%2Frllib%2Fexamples%2Fpolicy%2Frock_paper_scissors_dummies.py%22%2C%22np.int32%22%5D "venv/lib/python3.9/site-packages/ray/rllib/examples/policy/rock_paper_scissors_dummies.py")。

这个策略的目标是选择一个随机的动作，并在整个过程中坚持使用这个动作。这是通过在初始化时创建一个探索对象来实现的，这个探索对象会在每次调用时返回相同的动作。

至于输出，策略类通常不直接产生输出，而是提供了一些方法，如[`compute_actions`](command:_github.copilot.openSymbolInFile?%5B%22venv%2Flib%2Fpython3.9%2Fsite-packages%2Fray%2Frllib%2Fexamples%2Fpolicy%2Frock_paper_scissors_dummies.py%22%2C%22compute_actions%22%5D "venv/lib/python3.9/site-packages/ray/rllib/examples/policy/rock_paper_scissors_dummies.py")，[`learn_on_batch`](command:_github.copilot.openSymbolInFile?%5B%22venv%2Flib%2Fpython3.9%2Fsite-packages%2Fray%2Frllib%2Fexamples%2Fpolicy%2Frock_paper_scissors_dummies.py%22%2C%22learn_on_batch%22%5D "venv/lib/python3.9/site-packages/ray/rllib/examples/policy/rock_paper_scissors_dummies.py")等，这些方法在被调用时会产生输出。例如，[`compute_actions`](command:_github.copilot.openSymbolInFile?%5B%22venv%2Flib%2Fpython3.9%2Fsite-packages%2Fray%2Frllib%2Fexamples%2Fpolicy%2Frock_paper_scissors_dummies.py%22%2C%22compute_actions%22%5D "venv/lib/python3.9/site-packages/ray/rllib/examples/policy/rock_paper_scissors_dummies.py")方法会根据当前的状态和策略产生一个动作，[`learn_on_batch`](command:_github.copilot.openSymbolInFile?%5B%22venv%2Flib%2Fpython3.9%2Fsite-packages%2Fray%2Frllib%2Fexamples%2Fpolicy%2Frock_paper_scissors_dummies.py%22%2C%22learn_on_batch%22%5D "venv/lib/python3.9/site-packages/ray/rllib/examples/policy/rock_paper_scissors_dummies.py")方法会根据一个批量的经验进行学习并更新策略的参数。