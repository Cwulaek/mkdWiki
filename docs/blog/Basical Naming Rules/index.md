# Basical Naming Rules

这大概是给我看的。

你有意见，我没有。

没有意见才用这些。

## 基础部分

驼峰式: 大部分变量。

后缀 `(ust)`: `unstatic` 即为 非 `常量` ——意为私有变量。

后缀 `(nfs)`: `no freeze screen` 即为 不 `冻结屏幕`——仅对函数标注，意为未勾选 `不刷新屏幕`。

前缀 `xxx:`: xxx为作用域，一般用于一个函数的独有变量。  
例：AdjustCardData中使用变量i，写作acd:i。  

前缀 `~`/`~XXX`: 例如 `~ub:tempList`、`~RENDERgame:selecting?` 或 `~GUIplayerShop:goodsList`，第一级作用域一般较大且使用大写全名+驼峰子域名。  
标注全局变量/列表，用于代码块间交互。

大写式: 例如`CARD_DATA_TYPES`，一般等价于`enum`(枚举)，用于全局不改变的常量，一般为列表。
另外，部分该标注的列表被认为大多数情况下`只读`，仅在特殊情况下改变。

下划线式: 例如 `animate_tick`，一般代表 `非克隆体` 作用域下 `常量`。(现一般用驼峰式代替。)  
`URM` 引擎中 `Update` 部分改变了它，所以那部分已改作 `render:animateTick`

前缀 `~~`: 类似 `~`，但一般用于同种模块的不同克隆体间交互，较少用。  
一般字母使用小写。

前缀 `~~~`: 将变量/列表/函数标注为测试用途，一般字母使用大写。

驼峰式前缀: 部分情况下使用首字母标注前缀出现相同的情况，这时必须使用驼峰式前缀，但表意完全的情况下可省略部分单词的小写字母。

空格式函数：一般存在与 `add` 和 `new` 以及 `summon ... to stage`(用于动态克隆池)，分别表示注册、新建或帧动画。  
例：`add weapon`、`new fruit`、`summon card to stage`。一般不标注 `(ust)` 和 `(nfs)`。

省略式变量: 对于长单词，可用简写代替一部分单词。如 `positionedResourceLocationInbattleWithDimension` 可简写为 `POS_RES_LOC_inbattleWith_DIM` 或 `PRL_inbattleWith_D`。  
一般使用 _大写首字母串联、简写间无下划线_ 或 _大写长简称串联、简写间有下划线_。  
其中，只要一个地方左右存在需要下划线的情况，就需要下划线(开头末尾除外)。  
下划线后驼峰开头用小写。前后缀对该部分命名无影响。  
作用域可使用纯小写字母表示单词(不需下划线)或依照上述方案(单个字母作简称时可直接改为小写，需要填写的下划线不变)。

子函数: 对函数进行封装的过程中，仅用于对某函数的部分模块封装的情况下，可以使用子函数标注，这时可以自由使用父函数变量。  
当标注子函数时使用`::`中缀，当标注子函数的独有变量或子函数时使用`.`中缀。  
例：`drawCard` 的私有子函数 `drawData` 可写作 `dc::drawData(ust)`，子函数独有 `temp` 私有变量写作 `dc.drawData:temp(ust)`；`renderMap` 的子函数 `renderBlock` 可写作 `renderMap::renderBlock`，其循环变量 `i` 可写作 `renderMap.rb:i` 或 `renderMap:i`(这涉及到 `Render` 部分特殊命名规则)。

后缀 `?`: 表示布尔值，可用于变量和列表。

定长列表: 使用 `[x]` 作为后缀，x表示长度。用于提示使用时注意固定的长度不能随意改变。

选值变量/列表: 使用 `[a/b/c/...]` 作为后缀，其中每一项代表可填的内容。(现一般较少用。)~~正常来说没人会只限制一个值对吧？~~

前后缀共用: `(ust)(nfs)` 可写作 `(ust,nfs)`，先写 `?` 再写 `()`。`[x][a/b/c/...]`可写作`[x;a/b/c/...]`。

特殊功能变量/列表：  
1. 使用功能代替作用域放到前缀。如用 `player` 和 `enemy` 区分敌我。  
2. 一组变量/列表(一般为列表)来描述一个对象，作用域处填写对象种类。用于减少字符串拆解的复杂度。
3. 类似2，但作用域处需要复数。承载 `new` 在初始化部分添加的值。

大定义域特殊功能变量/列表: 一般带有 `(in...)`  
例如玩家魔力值，假设战斗结束后回满，此时需要在战斗中独有的玩家魔力值。可写作 `player:mp(inbattle)`。

前缀 `u-`、`w-`、`z-`: 用于常用函数更易获取。点击函数后的首个拓展(一般都有至少一个拓展吧?)后向上滑滚轮即可快速索引函数。(用处不大，三者区别未定义)

前缀 `#`: 一般用于引擎中，表示此变量请不要触及。一般无作用域，直接用小写(可带省略)+下划线或横线(单词间，强制)。

## 函数

### 枚举量

#### 注释型写法

在函数结尾使用`// 解释` 或 参数后使用 `/* 解释 */`。（如果你习惯 `Python` 等语言的其他注释写法，也可以使用）  

另外，单独在函数中第一行，使用注释块进行分行解释显然更美观，但可能稍显冗长。

#### 变量选值写法

与基础部分相似。仅在此处参数名不会过长（约20字符）时使用。

例如：`0=effect/1=card` 作参数名。

仅 `0/1` 时请使用布尔。

### 可选参数

这些函数应该标明可选的参数，以及如何选参。注意，这里并不包含可以填什么。

函数写法：  
`函数名 参数1 参数2 .. 参数n [表达式] [选参1] [选参2] ... [选参n]`

表达式的写法可以较为自由，你可以写让人能显而易见看懂的布尔表达式，也可以写较为复杂的正则表达式。  
当然，你也可以写中文。

**注意：表达式为空时恒成立。**

### 部分选参

举例函数 `findNext`，假如有 `当前now` `强制位置forcedNext` `强制坐标forcedNextPos`。

举三种情况。

若已知 `now` 必填，`forcedNext` 和 `forcedNextPos` 存在至少一个时可以正常执行函数。

此时函数的写法为：
`findNext now [forcedNext|forcedNextPos] [forcedNext] [forcedNextPos]`

若已知 `now` 必填，`forcedNext` 和 `forcedNextPos` 存在恰好一个时可以正常执行函数。

此时函数的写法为：
`findNext now [forcedNext^forcedNextPos] [forcedNext] [forcedNextPos]`

若已知 `now` 必填，`forcedNext` 和 `forcedNextPos` 存在至多一个时可以正常执行函数。

此时函数的写法为：
`findNext now [!(forcedNext&forcedNextPos)] [forcedNext] [forcedNextPos]`

### 完全选参

举例函数 `renderABC`，假如有 `高度height` `宽度width` `颜色colour` `编号id` `透明度transparency` `方向direction` 等参数。  

已知存在 `id` 时可以完全执行函数。同时，除 `id` `transparency` 以外同时存在时也可以执行函数。

此时函数的写法为：（我重排了参数，稍显美观）  
`renderABC [id|(height&weight&colour&direction)] [id] [height] [weight] [colour] [transparency] [direction]`

## URM部分

`Render`:  
  涉及该部分渲染的子函数变量的作用域需要全称驼峰，可省略子函数(此处指某部分Render函数)中的子函数(用于封装的函数)。  
  正常情况下函数不能使用 `()` 后缀。  
  此处不能更新非 `~` 数据(包括不能更改 `~~`)，可以修改 `client:hasRenderFinished?`。不可使用会造成等待的模块。

`Update`:  
  大致同Render。子函数变量作用域一般使用小写首字母简称。  
  此处一般用于判断输入、依照固定速率更新游戏。不可使用会造成等待、屏幕刷新的模块。

`Manipulate`:  
  这部分一般使用单个循环(`loop`)、广播或 `Events`。除非使用 `loop`，非子函数部分必须标注 `(ust,nfs)` 或 `(event)`(不要只标注而不关不刷新屏幕！！)。  
  此处用于处理 `Update` 发来的信息。一般使用单变量交互，名为 `GUI:result`。  
  检测时注意 `renderTab` 是否为当前 `Manipulation`，避免tab间信息读取时造成影响。  
  广播名称或 `Event` 名称可做作用域名称。此处仅用于发起不连续的变化以及对 `Render` 和 `Update` 的 `tab` 进行变更。

## 跳帧与克隆池结合部分



## 事件部分 Events

后缀`(event)`: 实际效果包含 `(ust,nfs)`，还传递了 `我是event` 或 `我与event密切相关` 的信息。  
与post easily相关的模块请使用空格式命名。  

名称中包含 `Event` 作为后缀，同时使用驼峰命名时，认为包含 `(event)`。  
如不包含，请单独使用 `(ust)`/`(nfs)`，或单独标注 `(ne)` 表示二者皆非。

## 频道部分 Channels

格式: `CHANNEL-` + `[side]` + `-` + `[identifier]` 用于表征一个频道。  
如 `CHANNEL-S-map` 和 `CHANNEL-C-map`。  
常见的 `[side]`:
`S` 服务端  
`C` 客户端  
`E` 一些引擎内部端  
`B` 舞台  
