# ICRA2018_SC2env_RL
* ICRA地图：v1.0
* 星际2客户端版本：4.0.2

#### 地图信息
默认玩家车辆出生2辆车，地图设定为3分钟，官方车全图寻找玩家车辆进行打击
- Red Space：玩家车出生点
- Blue Space：官方车出生点
- Bound area：暂无设置
- 缩放比：1：100

#### agent信息
agent模型来自SC2里的攻城坦克模型
- 血量：均为2000HP
- 伤害值：每发50HP
- 射速：未知 (大概1秒1个吧)
- 动作：移动，停止，攻击，选择
- 移速：4.25 (相对现实世界来说，算是一秒走4.25米吧)
- Score：分数计算参照ICRA规则

#### 环境配置
* Pysc2：https://github.com/deepmind/pysc2
* 星际争霸2客户端4.0.2：https://github.com/Blizzard/s2client-proto (推荐linux版本)

下载之后，将 **ICRA.sc2map** 放入 **StarcraftII/Maps/mini_games/** ,然后打开 **pysc2/maps/mini_games.py** 并添加地图名称 "ICRA",
现在你就可以运行和测试这个环境了，输入下面的命令赶紧试一试吧
```bash
$ python -m pysc2.bin.play --map ICRA
```

#### 4.0.2 version Replay的问题
参照以下之后即可运行
* https://github.com/deepmind/pysc2/issues/131 
* https://github.com/deepmind/pysc2/commit/fee7133a9abd8f1dfc90d5e7c2884cae04283eb7

既修改 **pysc2/run_configs/platforms.py** 里面的VERSIONS信息，添加
```python
VERSIONS = { 
  "4.0.2": (59877, "B43D9EE00A363DAFAD46914E3E4AF362"),
}
```
