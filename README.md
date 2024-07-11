# AI Pokemon/ AI Pocket Monster/ AI 宝可梦

## 简介
主体部分是通过python（~因为只会这个orz~）实现的，但是main函数则通过ipynb的格式编译以便结果显示和调试。项目大概写了一天半吧，因为我是编程新手，很多代码是直接请教的gpt。AI的API使用的是 *智谱* 的国产大模型（~因为送了Token~），可以自行更换调用模型相关代码（~尤其是绘图的模型，智谱的很垃圾~）。
	
整个项目包含4个部分：

1. 宝可梦生成（已完成）
2. 对战逻辑（已完成）
3. 游戏画面（完成一半）
4. 联机功能（写了几行）

## 宝可梦生成

![图片](https://github.com/GA10d/AI-Pokemon/assets/128725933/dea89d3c-4fee-4a63-bab3-b373fedd81c6)

### 宝可梦描述

玩家通过再 *playerA.txt* 文件的第一行写宝可梦的名字即可，如果想要详细宝可梦则可以在第二行写宝可梦的描述。如果游戏开始时，玩家没有输入宝可梦的描述，则AI会根据名字自动输入宝可梦的描述。

### 宝可梦技能和图标

**文本AI**根据宝可梦描述和名字会生成3个技能（~如果AI没发癫的话~）及技能描述（不包含数值逻辑），**绘图AI**会根据每个技能的名字和描述来生成对应的技能图标，并存储在 *playerA* 或 *playerB* 的文件夹里。

## 对战逻辑

先随机一个宝可梦先手，然后由玩家选择释放那个技能，**裁判AI（~经调教的文本AI~）**会根据双方宝可梦的特性来生成战斗的过程，并上传至log。可以通过以下代码生成游戏的log并在game_log.txt查看：

```
logloader.generate_log()
```

如果想手动技能（序号0、1、2）释放需要把上面注释的代码取消注释，然后删掉下面的代码：

```
# skill2use = input('选择要释放的技能')
skill2use = random.randint(0,len(movement.skill_name)-1)
```

## 游戏画面

*game_test.ipynb* 通过调用pygame来实现一个简单的宝可梦对战画面，目前已经实现了部分美术资源的调入，但是懒得写后面的逻辑了...

## 联机功能

*server* 文件夹中的代码参考的https://www.bilibili.com/video/BV15D421V7AG/?spm_id_from=333.337.search-card.all.click

我完全看不懂，只能照搬，而且没写几行，所以不多说了。

## 游戏log演示

```
[2024-07-12 00:15:23]: [system]: 游戏开始
[2024-07-12 00:15:34]: [system]: 检测到playerA没有写描述，已自动生成描述。
[2024-07-12 00:15:34]: [system]: playerA 玩家信息已录入
[2024-07-12 00:15:34]: [system]: playerA 宝可梦名字：闪电凤凰已录入
[2024-07-12 00:15:34]: [system]: playerA 宝可梦初始描述已录入
[2024-07-12 00:15:59]: [system]: playerA\playerA_monster.jpeg 宝可梦图片已录入
[2024-07-12 00:16:15]: [system]: playerA 生成了第1个技能图片（playerA_skill_icon1.jpeg）
[2024-07-12 00:16:25]: [system]: 检测到playerB没有写描述，已自动生成描述。
[2024-07-12 00:16:25]: [system]: playerB 玩家信息已录入
[2024-07-12 00:16:25]: [system]: playerB 宝可梦名字：水晶哆啦A梦已录入
[2024-07-12 00:16:25]: [system]: playerB 宝可梦初始描述已录入
[2024-07-12 00:16:40]: [system]: playerB\playerB_monster.jpeg 宝可梦图片已录入
[2024-07-12 00:16:54]: [system]: playerB 生成了第1个技能图片（playerB_skill_icon1.jpeg）
[2024-07-12 00:17:06]: [system]: playerB 生成了第2个技能图片（playerB_skill_icon2.jpeg）
[2024-07-12 00:17:17]: [system]: playerB 生成了第3个技能图片（playerB_skill_icon3.jpeg）
[2024-07-12 00:17:17]: [system]: 游戏开始初始化
[2024-07-12 00:17:17]: [system]: playerA先手
[2024-07-12 00:17:17]: [playerA]: playerA 释放了技能：[雷火焚身]
[2024-07-12 00:17:21]: [playerA]: 闪电凤凰迅速逼近水晶哆啦 A 梦，猛地展开双翅，雷电与火焰瞬间交织，化为一道毁灭性的光芒，将水晶哆啦 A 梦吞没。水晶哆啦 A 梦痛苦地哀嚎，被雷火焚身的效果所折磨，无力地跪倒在地。

[2024-07-12 00:17:22]: [playerB]: 水晶哆啦A梦 受到38点伤害
[2024-07-12 00:17:22]: [playerB]: 水晶哆啦A梦 剩余血量：62
[2024-07-12 00:17:22]: [playerB]: playerB 释放了技能：[智慧之光]
[2024-07-12 00:17:24]: [playerB]: 水晶哆啦 A 梦凝聚智慧和友情的能量，释放出耀眼的光芒，降低对手的攻击和特攻，并有机会让对手混乱，使其攻击自己或队友。

[2024-07-12 00:17:26]: [playerA]: 闪电凤凰 受到34点伤害
[2024-07-12 00:17:26]: [playerA]: 闪电凤凰 剩余血量：66
[2024-07-12 00:17:26]: [playerA]: playerA 释放了技能：[雷火焚身]
[2024-07-12 00:17:29]: [playerA]: 闪电凤凰聚集了全身的雷电和火焰能量，向水晶哆啦 A 梦发起猛烈攻击。水晶哆啦 A 梦被强大的力量震慑，暂时陷入瘫痪状态。

[2024-07-12 00:17:30]: [playerB]: 水晶哆啦A梦 受到33点伤害
[2024-07-12 00:17:30]: [playerB]: 水晶哆啦A梦 剩余血量：29
[2024-07-12 00:17:30]: [playerB]: playerB 释放了技能：[智慧之光]
[2024-07-12 00:17:32]: [playerB]: 水晶哆啦 A 梦凝聚智慧和友情的能量，释放出耀眼的光芒，降低对手的攻击和特攻，并有机会让对手混乱，使其攻击自己或队友。

[2024-07-12 00:17:34]: [playerA]: 闪电凤凰 受到53点伤害
[2024-07-12 00:17:34]: [playerA]: 闪电凤凰 剩余血量：13
[2024-07-12 00:17:34]: [playerA]: playerA 释放了技能：[雷火焚身]
[2024-07-12 00:17:51]: [playerA]: 宝可梦 A 释放出高度集中的雷电和火焰能量，这些能量迅速汇聚成一个巨大的火球，伴随着震耳欲聋的雷鸣声，火球以惊人的速度向宝可梦 B 射去。宝可梦 B 试图闪避，但火球的速度太快，它无法逃脱。就在火球即将击中宝可梦 B 的瞬间，一道耀眼的光芒突然闪过，火球瞬间被击散，消散在空气中。宝可梦 A 惊讶地看着这一幕，它不明白为什么自己的绝招会被如此轻松地化解。宝可梦 B 并没有趁机反击，而是微笑着看着宝可梦 A，似乎在等待它下一步的行动。宝可梦 A 并没有被挫败，它知道自己还有更强大的技能。它深吸一口气，然后大喊一声，全身被一股强大的电流所覆盖。宝可梦 A 身上的电光越来越强烈，最终形成了一道巨大的雷电，向宝可梦 B 猛扑过去。宝可梦 B 再次试图闪避，但这次它没有成功。雷电击中了宝可梦 B，瞬间让它瘫痪在地。宝可梦 A 成功地利用自己的技能取得了优势，但它并没有乘胜追击，而是选择了给宝可梦 B 一个机会。它知道，只有真正的强者才会给对手一个公平的机会。宝可梦 A 退后一步，等待着宝可梦 B 的再次挑战。宝可梦 B 从地上爬起来，眼中闪烁着坚定的光芒。它知道，这场战斗才刚刚开始。

[2024-07-12 00:17:52]: [playerB]: 水晶哆啦A梦 受到28点伤害
[2024-07-12 00:17:52]: [playerB]: 水晶哆啦A梦 剩余血量：1
[2024-07-12 00:17:52]: [playerB]: playerB 释放了技能：[未来之击]
[2024-07-12 00:17:54]: [playerB]: 水晶哆啦 A 梦使用了未来之击！

[2024-07-12 00:17:55]: [playerA]: 闪电凤凰 受到25点伤害
[2024-07-12 00:17:55]: [system]: 水晶哆啦A梦 获胜
```

## 智谱的网址
https://open.bigmodel.cn/overview
