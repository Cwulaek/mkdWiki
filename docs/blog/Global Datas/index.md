# Global Datas

全局处理，私有同步，里外分开。

## 全局处理

`GlobalData` 单独对所有相关的 `event` 去保存修改、记录行为、统计次数等。

+ ## 私有同步

`GlobalData` 自己在更新时发送 `event`，告知相关存储对象更新行为。

## 里外分开
不同 `GlobalData` 的作用域不同，切记。

做好 `GlobalData` 与 `saveRequired` 数据的区别。

