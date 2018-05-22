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
- 血量：均为2000HP
- Damage：每发50HP
- 射速：未知 (大概1秒1个吧)
- 动作：移动，停止，攻击，选择
- 移速：4.25 (相对现实世界来说，算是一秒走4.25米吧)
- Score：分数计算参照ICRA规则

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

既修改 **pysc2/run_configs/platforms.py** 里面的VERSIONS信息，添加
```python
VERSIONS = { 
  "4.0.2": (59877, "B43D9EE00A363DAFAD46914E3E4AF362"),
}
```

## ICRA_pysc2环境运行例程

<div align="center">
  <img src=images/ICRA.gif width="720px"/>
</div>

这个算法根据DeepMind的PySC2-RL-A3C算法定义的，论文链接[paper](https://deepmind.com/documents/110/sc2le.pdf),
代码来自于南开大学dalao [xhujoy](https://github.com/xhujoy/pysc2-agents)的(99.99%一样)，他的[知乎](https://zhuanlan.zhihu.com/p/29246185?group_id=890682069733232640)

### 环境
* tensorflow(适配GPU版本)
* s2clientprotocol（见上面）
* pysc2（见上面）
* absl-py
```shell
pip install absl-py
pip install tensorflow-gpu
```

### 安装
```shell
git clone https://github.com/PeterLayton/ICRA2018_SC2env_RL
cd ICRA2018_SC2env_RL
```
### 测试
输入以下指令即可开始training，大概会花上2天1夜，将产生**20G**左右的model文件，注意空间
```shell
python -m main
```
训练完成后，输入以下指令可看结果
```shell
python -m main --training=False
```

<div align="center">
  <img src=images/sroce.png width="910px"/>
</div>

上图为此算法6000次的测试结果，平均上下限为2000分至3500分
