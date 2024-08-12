# 实际代码案例分析

对我目前编写的项目进行分块说明。（当然，随着项目不断开发，仍有待完善）

主要分 `Server`/`Client`，同时会在内部再细分。（均为双角色）

`Server` 负责数据操作，`Client` 负责渲染及相关交互。  
`Client` 不能直接修改数据，需要发包。（`Event`/`Channels`）  

所以你可以在 `Server` 部分找到复杂的逻辑部分，在 `Client` 找到动画、侦测相关实现。

存在 `S` 与 `C` 的对应时，会有单独的按钮帮助跳转。

[**Codemon**](./Codemon/index.md)

[**DCard:Legend**](./DCard_Legend/index.md)

[**Parabox**](./Parabox/index.md)

# 以下使用旧引擎

这部分可能不会进行说明。

ISOBALL  

CardWars I  

Clash of Balls
