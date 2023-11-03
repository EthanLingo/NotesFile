



# 文档里的几种环境

## Battle

```{figure} battle.gif
:width: 140px
:name: battle
```

| Import             | `from magent2.environments import battle_v4` |
|--------------------|-------------------------------------------|
| Actions            | Discrete                                  |
| Parallel API       | Yes                                       |
| Manual Control     | No                                        |
| Agents             | `agents= [red_[0-80], blue_[0-80]]`       |
| Agents             | 162                                       |
| Action Shape       | (21)                                      |
| Action Values      | Discrete(21)                              |
| Observation Shape  | (13,13,5)                                 |
| Observation Values | [0,2]                                     |
| State Shape        | (45, 45, 5)                               |
| State Values       | (0, 2)                                    |

A large-scale team battle. Agents are rewarded for their individual performance, and not for the performance of their neighbors, so coordination is difficult.  Agents slowly regain HP over time, so it is best to kill an opposing agent quickly. Specifically, agents have 10 HP, are damaged 2 HP by
each attack, and recover 0.1 HP every turn.

Like all MAgent2 environments, agents can either move or attack each turn. An attack against another agent on their own team will not be registered.

### Arguments

``` python
battle_v4.env(map_size=45, minimap_mode=False, step_reward=-0.005,
dead_penalty=-0.1, attack_penalty=-0.1, attack_opponent_reward=0.2,
max_cycles=1000, extra_features=False)
```

`map_size`: Sets dimensions of the (square) map. Increasing the size increases the number of agents. Minimum size is 12.

`minimap_mode`: Turns on global minimap observations. These observations include your and your opponents piece densities binned over the 2d grid of the observation space. Also includes your `agent_position`, the absolute position on the map (rescaled from 0 to 1).


`step_reward`:  reward after every step

`dead_penalty`:  reward when killed

`attack_penalty`:  reward when attacking anything

`attack_opponent_reward`:  reward added for attacking an opponent

`max_cycles`:  number of frames (a step for each agent) until game terminates

`extra_features`: Adds additional features to observation (see table). Default False

#### Action space

Key: `move_N` means N separate actions, one to move to each of the N nearest squares on the grid.

Action options: `[do_nothing, move_12, attack_8]`

#### Reward

Reward is given as:

* 5 reward for killing an opponent
* -0.005 reward every step (step_reward option)
* -0.1 reward for attacking (attack_penalty option)
* 0.2 reward for attacking an opponent (attack_opponent_reward option)
* -0.1 reward for dying (dead_penalty option)

If multiple options apply, rewards are added.

#### Observation space

The observation space is a 13x13 map with the below channels (in order):

feature | number of channels
--- | ---
obstacle/off the map| 1
my_team_presence| 1
my_team_hp| 1
my_team_minimap(minimap_mode=True)| 1
other_team_presence| 1
other_team_hp| 1
other_team_minimap(minimap_mode=True)| 1
binary_agent_id(extra_features=True)| 10
one_hot_action(extra_features=True)| 21
last_reward(extra_features=True)| 1
agent_position(minimap_mode=True)| 2

### State space

The observation space is a 45x45 map. It contains the following channels, which are (in order):

feature | number of channels
--- | ---
obstacle map| 1
team_0_presence| 1
team_0_hp| 1
team_1_presence| 1
team_1_hp| 1
binary_agent_id(extra_features=True)| 10
one_hot_action(extra_features=True)|  21
last_reward(extra_features=True)| 1


### Version History

* v0: Initial MAgent2 release (0.3.0)





## Battlefield

```{figure} battlefield.gif
:width: 140px
:name: battlefield
```

| Import             | `from magent2.environments import battlefield_v4` |
|--------------------|------------------------------------------------|
| Actions            | Discrete                                       |
| Parallel API       | Yes                                            |
| Manual Control     | No                                             |
| Agents             | `agents= [red_[0-11], blue_[0-11]]`            |
| Agents             | 24                                             |
| Action Shape       | (21)                                           |
| Action Values      | Discrete(21)                                   |
| Observation Shape  | (13,13,5)                                      |
| Observation Values | [0,2]                                          |
| State Shape        | (80, 80, 5)                                    |
| State Values       | (0, 2)                                         |


Same as [battle](./battle) but with fewer agents arrayed in a larger space with obstacles.

A small-scale team battle, where agents have to figure out the optimal way to coordinate their small team in a large space and maneuver around obstacles in order to defeat the opposing team. Agents are rewarded for their individual performance, and not for the performance of their neighbors, so
coordination is difficult.  Agents slowly regain HP over time, so it is best to kill an opposing agent quickly. Specifically, agents have 10 HP, are damaged 2 HP by each attack, and recover 0.1 HP every turn.

Like all MAgent2 environments, agents can either move or attack each turn. An attack against another agent on their own team will not be registered.

### Arguments

``` python
battle_v4.env(map_size=80, minimap_mode=False, step_reward-0.005,
dead_penalty=-0.1, attack_penalty=-0.1, attack_opponent_reward=0.2,
max_cycles=1000, extra_features=False)
```

`map_size`: Sets dimensions of the (square) map. Minimum size is 46.

`minimap_mode`: Turns on global minimap observations. These observations include your and your opponents piece densities binned over the 2d grid of the observation space. Also includes your `agent_position`, the absolute position on the map (rescaled from 0 to 1).

`step_reward`:  reward added unconditionally

`dead_penalty`:  reward added when killed

`attack_penalty`:  reward added for attacking

`attack_opponent_reward`:  Reward added for attacking an opponent

`max_cycles`:  number of frames (a step for each agent) until game terminates

`extra_features`: Adds additional features to observation (see table). Default False

#### Action Space

Key: `move_N` means N separate actions, one to move to each of the N nearest squares on the grid.

Action options: `[do_nothing, move_12, attack_8]`

#### Reward

Reward is given as:

* 5 reward for killing an opponent
* -0.005 reward every step (step_reward option)
* -0.1 reward for attacking (attack_penalty option)
* 0.2 reward for attacking an opponent (attack_opponent_reward option)
* -0.1 reward for dying (dead_penalty option)

If multiple options apply, rewards are added.

#### Observation space

The observation space is a 13x13 map with the below channels (in order):

feature | number of channels
--- | ---
obstacle/off the map| 1
my_team_presence| 1
my_team_hp| 1
my_team_minimap(minimap_mode=True)| 1
other_team_presence| 1
other_team_hp| 1
other_team_minimap(minimap_mode=True)| 1
binary_agent_id(extra_features=True)| 10
one_hot_action(extra_features=True)| 21
last_reward(extra_features=True)| 1
agent_position(minimap_mode=True)| 2

### State space

The observation space is a 80x80 map. It contains the following channels, which are (in order):

feature | number of channels
--- | ---
obstacle map| 1
team_0_presence| 1
team_0_hp| 1
team_1_presence| 1
team_1_hp| 1
binary_agent_id(extra_features=True)| 10
one_hot_action(extra_features=True)|  21
last_reward(extra_features=True)| 1



### Version History

* v0: Initial MAgent2 release (0.3.0)





## Adversarial Pursuit

```{figure} adversarial_pursuit.gif
:width: 140px
:name: adversarial_pursuit
```

| Import             | `from magent2.environments import adversarial_pursuit_v4` |
|--------------------|--------------------------------------------------------|
| Actions            | Discrete                                               |
| Parallel API       | Yes                                                    |
| Manual Control     | No                                                     |
| Agents             | `agents= [predator_[0-24], prey_[0-49]]`               |
| Agents             | 75                                                     |
| Action Shape       | (9),(13)                                               |
| Action Values      | Discrete(9),(13)                                       |
| Observation Shape  | (9,9,5), (10,10,9)                                     |
| Observation Values | [0,2]                                                  |
| State Shape        | (45, 45, 5)                                            |
| State Values       | (0, 2)                                                 |


The red agents must navigate the obstacles and tag (similar to attacking, but without damaging) the blue agents. The blue agents should try to avoid being tagged. To be effective, the red agents, who are much are slower and larger than the blue agents, must work together to trap blue agents so
they can be tagged continually.

### Arguments

``` python
adversarial_pursuit_v4.env(map_size=45, minimap_mode=False, tag_penalty=-0.2,
max_cycles=500, extra_features=False)
```

`map_size`: Sets dimensions of the (square) map. Increasing the size increases the number of agents. Minimum size is 7.

`minimap_mode`: Turns on global minimap observations. These observations include your and your opponents piece densities binned over the 2d grid of the observation space. Also includes your `agent_position`, the absolute position on the map (rescaled from 0 to 1).

`tag_penalty`:  reward when red agents tag anything

`max_cycles`:  number of frames (a step for each agent) until game terminates

`extra_features`: Adds additional features to observation (see table). Default False

#### Action Space

Key: `move_N` means N separate actions, one to move to each of the N nearest squares on the grid.

Predator action options: `[do_nothing, move_4, tag_8]`

Prey action options: `[do_nothing, move_8]`

#### Reward

Predator's reward is given as:

* 1 reward for tagging a prey
* -0.2 reward for tagging anywhere (`tag_penalty` option)

Prey's reward is given as:

* -1 reward for being tagged


#### Observation space

The observation space is a 10x10 map for pursuers and a 9x9 map for the pursued. They contain the following channels, which are (in order):

feature | number of channels
--- | ---
obstacle/off the map| 1
my_team_presence| 1
my_team_hp| 1
other_team_presence| 1
other_team_hp| 1
binary_agent_id(extra_features=True)| 10
one_hot_action(extra_features=True)| 9/Prey,13/Predator
last_reward(extra_features=True)| 1

### State space

The observation space is a 45x45 map. It contains the following channels, which are (in order):

feature | number of channels
--- | ---
obstacle map| 1
prey_presence| 1
prey_hp| 1
predator_presence| 1
predator_hp| 1
binary_agent_id(extra_features=True)| 10
one_hot_action(extra_features=True)|  13 (max action space)
last_reward(extra_features=True)| 1


### Version History

* v0: Initial MAgent2 release (0.3.0)