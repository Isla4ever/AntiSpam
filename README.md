# AntiSpam
原作者为[元路](https://www.mcbbs.net/home.php?mod=space&uid=670070)(膜拜大佬)，该插件为[yuanluAntiSpam](https://www.mcbbs.net/thread-903631-1-1.html)的Nukkit实现版，以下内容为原帖介绍  
![GitHub All Releases](https://img.shields.io/github/downloads/Isla4ever/AntiSpam/total)  
**下载在[Release](https://github.com/Isla4ever/AntiSpam/releases)里**

## 介绍

元路反刷屏插件是一款能够智能拦截玩家聊天的插件
本插件通过玩家近期话语相似度判断、话语间转换难度、整句信息熵计算、平均信息熵计算
来智能拦截玩家发言是否存在刷屏、无意义行为

插件具有以下特点:

高自定义度 - 插件中所有信息均可自定义，让插件更适合您的服务器 

高效性 - 本人非常注重代码运行效率，已尽可能地优化了速度，对服务器影响可忽略不计 

智能性 - 引用了2类共4种刷屏信息判定方式，极大地减少刷屏信息 可拓展性 - 本插件开源并提供javadoc，方便各位学习及改进

## 原理介绍

1. 信息熵

   信息熵简介:

   > 信息是个很抽象的概念。人们常常说信息很多，或者信息较少，但却很难说清楚信息到底有多少。比如一本五十万字的中文书到底有多少信息量。
   > 直到1948年，香农提出了“信息熵”的概念，才解决了对信息的量化度量问题。信息熵这个词是C．E．香农从热力学中借用过来的。热力学中的热熵是表示分子状态混乱程度的物理量。香农用信息熵的概念来描述信源的不确定度。
   > 信息论之父克劳德·艾尔伍德·香农第一次用数学语言阐明了概率与信息冗余度的关系。

   信息熵的基本内容:

   ![image.png](https://i.loli.net/2020/08/31/ebZEhku1dNCGX94.png)

   　　由定义我们可知，当玩家的一句话中重复很多时，其信息熵会降低，由此我们可以通过信息熵来判断玩家说话是否有意义
   　　但由此直接判定玩家说话是否有意义不太公平(所以默认整句话信息熵是不被启用的)
   　　例如: "我的世界"与"我的世界我的世界"信息熵均为2.0，当玩家反复复制一段文字时也会显得有些无意义
   　　由此，我设想了一种方法，即，平均信息熵，此值为整体信息熵平均到每一个字符上的结果，但由于信息熵并非线性数值，所以我将话语长度取ln值后再带入除数，即得到平均信息熵
   　　公式如下: aH = (-∑Pi*log2(Pi))/ln(Length)
   　　注意：在我想出此方法前并没有注意到网上已经有了平均信息熵的概念，所以此公式并非通用公式

   ​		我在网上找到的平均信息熵解释: ([图片来源](https://www.mcbbs.net/plugin.php?id=link_redirect&target=https%3A%2F%2Fwww.jianshu.com%2Fp%2Fb841dbe21bd9))

   ![image](https://i.loli.net/2020/04/16/kuQIW9gNBhr7fjs.jpg)

2. 相似度

　　相似度通过计算两字符串之间的编辑转换距离再除以两字符串中最长的一个长度得出
　　插件将会缓存玩家近期聊天数据(数量由配置文件决定)然后再进行比对
　　编辑转换距离计算方法如下:

​		![image](https://i.loli.net/2020/04/16/pfEPTiWDs29ndvX.png)

3. 命令

　插件提供了多种命令来满足您对玩家刷屏限制的需求
　对于命令您亦可在游戏中查看帮助
　*命令工具类: yuanluCommand,版本:1.0.0 (id:1)*
　所有命令均需玩家拥有yuanlu.antiSpam.admin权限才可执行
　此权限也为此插件唯一权限

　/yantispam reload 重载配置文件
　/yantispam test ... 测试某(几)段话的信息熵、相似度信息, 您可以用#分割多段话
　/yantispam set <player> 将玩家配置设为默认
　/yantispam set <player> <name> 将玩家配置设为已有的某配置
　/yantispam set <player> <datas> 为某玩家设置独立的配置

|                 | minLength         | 判断最短长度           |
| --------------- | ----------------- | ---------------------- |
|                 | minAverageEntropy | 最小平均信息熵         |
|                 | minEntropy        | 最小信息熵             |
| 1:datas所需信息 | checkAmount       | 相似检查数量           |
|                 | maxSimilarity     | 最大相似度             |
|                 | minDistance       | 最小变换次数           |
|                 | time              | 近期消息缓存时间(毫秒) |

4. 图片展示

　话语信息熵计算:
　*更多信息已被隐藏*

![image](https://miao.su/images/2019/08/17/QQ20190817135335473db.png)

　内容无意义行为:
　 *聊天栏为触发的文字*

![image](https://s2.ax1x.com/2019/08/17/mnoQr4.png)

　内容过于相似行为:
　*聊天栏为触发文字*

![image](https://s2.ax1x.com/2019/08/17/mnolqJ.png)

　配置文件截图:
　*具体配置请详见config.yml文件*

![image](https://i.loli.net/2019/08/17/QiwODe8YqSuVfzX.png)

5. 下载

**在[Release](https://github.com/Isla4ever/AntiSpam/releases)里**
