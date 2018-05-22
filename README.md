

# ICRA2018_SC2env_RL
* Mini-game map made in ICRA：v1.0
* Starcraft 2 client version：4.0.2

## Mini-game information

### Description
The goal is that a  fully observable agent must find the other in order to start a battle 
- Bound area：No settings : 
- Scale ratio：1：100

### Initial State 
*   2 Hellions at at Red Space ( Agent )
*   2 Hellions at at Blue Space 

### Rewards 

### End Condition
Time Elapsed ( 180 seconds ) 

## agent information 
The agent model comes from the siege tank model in SC2
- Blood volume ：均为2000HP
- Damage：50HP 
- 射速：未知 (大概1秒1个吧) ( Don´t really get what Rate of Fire means here)
- Actions : Move, Stop, Attack, Select 
- Speed：4.25 
- Score：The score calculation refers to ICRA rules 

## Environment configuration 
Clone the pySC2 repository and install Starcraft 2 client 
* Pysc2：https://github.com/deepmind/pysc2
* Starcraft 2 Client 4.0.2：https://github.com/Blizzard/s2client-proto (推荐linux版本)

Download the ICRA.sc2map file and place it in the folder StarcraftII/Maps/mini_games
Add ICRA to the mini-games array in pysc2/maps/mini_games.py 
For any more detailed information visit this page 
```bash
$ python -m pysc2.bin.play --map ICRA
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


This algorithm is based on DeepMind´s PySC2-RL-A3C linked[paper](https://deepmind.com/documents/110/sc2le.pdf),
The code comes from [xhujoy](https://github.com/xhujoy/pysc2-agents)的(99.99%一样)，他的[知乎](https://zhuanlan.zhihu.com/p/29246185?group_id=890682069733232640)

### Requirements 
* tensorflow(适配GPU版本)
* s2clientprotocol（见上面）
* pysc2（见上面）
* absl-py
```shell
pip install absl-py
pip install tensorflow-gpu
```

### Installation 
```shell
git clone https://github.com/PeterLayton/ICRA2018_SC2env_RL
cd ICRA2018_SC2env_RL
```
### Test
Enter the following command to start training, it has taken about 3 days and might generate a 20 G model file 
```shell
python -m main
```
After the training phase is completed, enter the following instructions to see the results 
```shell
python -m main --training=False
```

<div align="center">
  <img src=images/sroce.png width="910px"/>
</div>

The above figure shows the results of 6000 tests for this algorithm. The average upper and lower limits are  ranged from 2000 to 3500 points
