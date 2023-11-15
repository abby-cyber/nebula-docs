# 服务管理

在服务管理页面，用户可以查看服务的 Host、路径、状态等信息，还可以启动、停止、强杀、重启服务，并且可以方便快捷地查看日志文件内容。

## 入口

1. 在{{dashboard_ent.name}}顶部导航栏，单击**集群管理**。
2. 单击目标集群右侧**详情**。
3. 在左侧导航栏，单击**集群操作**->**服务管理**。

## 操作说明

!!! danger

    单击**停止**/**重启**，会立即中断进行中的任务，可能会导致数据不一致，请在业务低峰期执行该操作。

- 找到目标服务，在**操作**列进行相关操作。

- 勾选多个服务，在上方进行批量操作。

- 单击 ![nav](https://docs-cdn.nebula-graph.com.cn/figures/nav-dashboard_cn.png) 图标，可快速查看[服务监控信息](../2.monitor.md)。

- 进行数据同步时，可以在**依赖服务**页面查看及管理相关的服务。关于数据同步的详情，参见[集群间数据同步](../../../synchronization-and-migration/replication-between-clusters.md)。