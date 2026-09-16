# panda-board-data

panda-board 的**数据仓库**兼**静态网站发布源**。

```text
data/
  stocks/<code>.json      每只股票一份：基础信息 / 公告 / K线 / 市值
  meta/update.json        最近一次更新的状态与统计
  meta/export.json        导出计数
  meta/fetch_days.json    逐日采集完整性记录
  meta/board_meta.json    键值元数据
docs/                     GitHub Pages 发布目录（Branch: main, Folder: /docs）
                          ★ Pages 分支发布只支持 / 或 /docs，不支持 /site
```

## 写入方式

由 PandaStack 的**一次性沙箱**写入：clone 本仓库 → 导入临时 SQLite →
采集 → 建站 → 导出 → 一个原子提交。沙箱随即销毁，不保留任何状态。

**采集、建站、校验任一环节失败就不提交**，Pages 上始终保留上一份可用版本。

## 内容边界

只存公开的结构化数据：股票代码、公告标题/日期/链接、K 线、市值、采集元数据。
**不存**公告正文、PDF、附件、图片。

仓库内不含任何凭据——Token 只存在于 PandaStack Function 的 bundle 中。
