---
title:
  - RLlib 各种超参数解读
authors: Ethan Lin
year: 2024-04-09
tags:
  - 类型/笔记
  - 日期/2024-04-09
  - 学科/人工智能
  - 内容/计算科学
  - 内容/机器学习
  - 内容/工具/RLlib
  - 类型/AI问答笔记
---
# RLlib 各种超参数解读






> [!attention]
> 以下由AI回答，不保证正确性！







RLlib 当中，
```
config = (
                    PPOConfig()
                    .environment(
                        env=env_name,
                        clip_actions=True,
                        clip_rewards=True,
                        disable_env_checking=False,
                    )
                    .resources(num_gpus=int(os.environ.get("RLLIB_NUM_GPUS", "0")))
                    .rollouts(
                        num_rollout_workers=0,  # 模拟器的数量
                        num_envs_per_worker=1,  # 每个模拟器的环境数量
                        rollout_fragment_length=32,  # 每个训练批次的长度
                    )
                    # .debugging(log_level="ERROR")
                    .reporting(metrics_num_episodes_for_smoothing=1)
                    .training(
                        train_batch_size=32,  # 训练批次大小 #TODO 超参数调参，归一化
                        lr=2e-4,  # 学习率
                        gamma=0.99,  # 折扣因子
                        lambda_=0.9,  # GAE 折扣因子
                        use_gae=True,  # 是否使用 GAE
                        clip_param=0.4,  # PPO 损失函数的 clip 参数
                        grad_clip=None,  # 梯度裁剪
                        entropy_coeff=0.1,  # 熵系数
                        vf_loss_coeff=0.25,  # 值函数损失系数
                        sgd_minibatch_size=4,  # SGD 小批量大小
                        num_sgd_iter=10,  # SGD 迭代次数
                    )
                )
```
当中的 `rollout_fragment_length`、`train_batch_size`、`lambda`、`sgd_minibatch_size`、`num_sgd_iter` 分别是什么参数？都有什么联系与区别？


这些参数在PPO算法中都扮演着重要的角色,让我一一解释:

1. `rollout_fragment_length`: 这个参数决定了每个采样批次(rollout)的长度,即采样多少个环境步长。它决定了训练时的时间序列长度。较大的值可以提高采样效率,但过大可能会导致训练不稳定。

2. `train_batch_size`: 这个参数决定了每次梯度更新时使用的样本数量。它影响了训练的稳定性和收敛速度。较大的batch size可以提高训练效率,但过大可能会导致过拟合。

3. `lambda`: 这是GAE(Generalized Advantage Estimation)算法中的一个参数,它决定了时间差分价值函数估计的偏差和方差的权衡。它取值范围为`[0, 1]`,越大偏差越小但方差越大。

4. `sgd_minibatch_size`: 这个参数决定了每次SGD(随机梯度下降)迭代时使用的样本数量。它影响了训练的稳定性和收敛速度。较小的值可以提高训练稳定性,但可能会降低训练效率。

5. `num_sgd_iter`: 这个参数决定了每次训练批次中SGD的迭代次数。它影响了训练的收敛速度。较大的值可以提高训练效果,但可能会导致过拟合。

总的来说,这些参数都是PPO算法中的超参数,需要根据具体问题进行调参优化。它们之间存在一定的联系和权衡,需要综合考虑才能找到最佳配置。

GAE是一种用于估计环境奖励的优势函数的方法,它能够平衡偏差和方差,从而提高训练的稳定性和效果。

`lambda_`是GAE中的折扣因子,取值范围为[0, 1]。它决定了时间差分价值函数估计的偏差和方差的权衡。较大的值会减小偏差但增大方差,反之亦然。0.9是一个常用的折扣因子。

`use_gae` 则是决定是否使用GAE来估计优势函数。使用GAE相比直接使用Monte-Carlo方法通常能获得更好的性能。
    

总的来说,这两个参数都是PPO算法中用于优化优势函数估计的重要超参数。合理设置它们可以提高PPO算法的收敛速度和训练稳定性。

`entropy_coeff`: 这个参数控制了策略熵的权重。策略熵反映了策略的随机性,较高的熵意味着更好的探索能力。这个参数越大,算法会越倾向于保持较高的探索程度,防止过早收敛到局部最优。但过大会影响收敛速度。0.1是一个常用的值。
    
`vf_loss_coeff`: 这个参数控制了值函数损失在总损失中的权重。值函数损失用于优化价值函数网络,帮助算法更好地估计状态价值。这个参数越大,算法会更加关注值函数的拟合效果。但过大可能会导致策略优化受到影响。0.25 是一个常用的折中值。
    

总的来说,这两个参数是用来平衡策略优化和值函数拟合的权重的超参数。通过合理设置它们,可以使PPO算法在探索和利用之间达到平衡,提高整体的训练效果。

#### `train_batch_size` 与 `sgd_minibatch_size` 都是训练批次大小，那么二者区别是什么？

`train_batch_size` 和 `sgd_minibatch_size` 都是用于训练的批次大小，但它们在训练过程中的应用场景和作用是不同的。

- `train_batch_size`：这是用于训练的样本批次的大小。这些样本是从多个环境中收集的，每个环境提供 `rollout_fragment_length` 个样本。这个参数决定了每次更新模型参数时使用的样本数量。例如，如果 `train_batch_size` 是 4000，那么每次更新模型参数时将使用 4000 个样本。

- `sgd_minibatch_size`：这是每个随机梯度下降（SGD）迭代中使用的样本批次的大小。在每次 SGD 迭代中，会从 `train_batch_size` 大小的样本中随机抽取 `sgd_minibatch_size` 大小的样本来进行梯度计算和模型参数更新。例如，如果 `sgd_minibatch_size` 是 200，那么每次 SGD 迭代将从 4000 个样本中随机抽取 200 个样本来进行计算和更新。

总的来说，`train_batch_size` 控制了每次更新模型参数时使用的总样本数量，而 `sgd_minibatch_size` 控制了每次 SGD 迭代时使用的样本数量。在实际应用中，`sgd_minibatch_size` 通常会小于 `train_batch_size`，这是因为 SGD 是一种随机优化算法，每次只需要一部分样本就可以进行有效的参数更新。


#### `rollout_fragment_length` 设置采样的步长，如果太大超过环境终局的实际步长，要怎么处理呢？如果过小以至于没能到达环境终局的实际步长，程序内部会怎么处理呢？

如果`rollout_fragment_length`设置的步长超过了环境的实际步长，RLlib会在每个模拟器的环境中重置环境并继续采样，直到达到`rollout_fragment_length`为止。这意味着即使超过了环境的终局，RLlib仍会继续采样直到达到指定的步长。

如果`rollout_fragment_length`设置的值过小，导致无法采样到环境的终局步长，RLlib会根据`batch_mode`参数来确定如何处理。如果`batch_mode`设置为"truncate_episodes"，则会截断未完成的episode，并将其作为一次采样；如果设置为"complete_episodes"，则会等待直到完成整个episode，然后再进行采样。因此，可以根据具体的应用场景和需求来设置`batch_mode`参数，以达到合适的采样处理方式。