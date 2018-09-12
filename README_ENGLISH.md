# ICRA2018_SC2env_RL

* Mini-game map made in ICRA：v1.0
* Starcraft 2 client version：4.0.2

## Mini-game information

### Description

The map is created for competition of ICRA.
Both sides have two RoboMaster AI robots when the game start.
One side is the official AI robots (created at Red Space).
On the other side is the AI robots controlled by player (created at Blue Space).

The goal is that a fully observable agent must find the other in order to start a battle.

* Bound area：No settings : (is a treatment area in the ICRA rules)
* Scale ratio：1：100

### Initial State

* 2 Hellions at at Red Space ( Agent )
  * have full view to attack player's robots
* 2 Hellions at at Blue Space

### Rewards

Score count is followed the ICRA rules

$$ Score = α * x + β * Y - γ * Z $$

* X is the HP reduction of RoboMaster AI robots ( Agent ).
* Y is the remaining time ( in seconds ) when both RoboMaster AI robots are destroyed. If the challenge time ends before both AI robots are destroyed, Y is 0.
* Z is the HP reduction of Team Robots.

### End Condition

Time Elapsed ( 180 seconds )

## agent information

The agent model comes from the siege tank model in SC2

* Blood volume ：both 2000HP
* Damage：50HP per shot
* Rate of Fire: Unknown ( Approximately 1 second 1 )
* Actions : Move, Stop, Attack, Select
* Speed：4.25
* Score：The score calculation refers to ICRA rules

## Environment configuration

Clone the pySC2 repository and install Starcraft 2 client

* Pysc2：https://github.com/deepmind/pysc2
* Starcraft 2 Client 4.0.2：https://github.com/Blizzard/s2client-proto (Recommended linux version)

Download the ICRA.sc2map file and place it in the folder StarcraftII/Maps/mini_games.
Add ICRA to the mini-games array in pysc2/maps/mini_games.py.
For any more detailed information visit this page.

```bash
python -m pysc2.bin.play --map ICRA
```

## 4.0.2 version Replay Issues

Refer bellow to run

* https://github.com/deepmind/pysc2/issues/131 
* https://github.com/deepmind/pysc2/commit/fee7133a9abd8f1dfc90d5e7c2884cae04283eb7

Modify VERSIONS information in **pysc2/run_configs/platforms.py** adding :

```python
VERSIONS = {
  "4.0.2": (59877, "B43D9EE00A363DAFAD46914E3E4AF362"),
}
```

## ICRA_pysc2 environment running procedure

<div align="center">
  <img src=images/ICRA.gif width="720px"/>
</div>

This algorithm is based on DeepMind´s PySC2-RL-A3C linked [paper](https://deepmind.com/documents/110/sc2le.pdf),
The code comes from [xhujoy](https://github.com/xhujoy/pysc2-agents)(99.99%), his [knowing](https://zhuanlan.zhihu.com/p/29246185?group_id=890682069733232640)

### Requirements

* tensorflow ( GPU Adapted )
* s2clientprotocol ( See above )
* pysc2 ( See above )
* numpy ( maybe )
* absl-py

```bash
pip install absl-py
pip install tensorflow-gpu
```

or install via requirements.txt

### Installation

```bash
git clone https://github.com/PeterLayton/ICRA2018_SC2env_RL
cd ICRA2018_SC2env_RL
```

### Test

Enter the following command to start training, it has taken about 3 days and might generate a 20 G model file

```bash
python -m main
```

After the training phase is completed, enter the following instructions to see the results

```bash
python -m main --training=False
```

<div align="center">
  <img src=images/sroce.png width="910px"/>
</div>

The above figure shows the results of 6000 tests for this algorithm. The average upper and lower limits are  ranged from 2000 to 3500 points
