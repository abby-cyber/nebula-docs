# 节点管理

节点管理页面展示所有的节点详情信息，包括节点名称、Host 及 SSH 用户名称、Zone、CPU 核等信息，并且支持添加节点、管理节点服务等操作。

## 注意事项

如果启用了 Zone 功能，添加节点时必须为节点选择所属的 Zone。添加节点后，无法修改节点所属 Zone，只能缩容移除节点后重新添加节点。

## 入口

1. 在{{dashboard_ent.name}}顶部导航栏，单击**集群管理**。
2. 单击目标集群右侧**详情**。
3. 在左侧导航栏，单击**集群操作**->**节点管理**。

## 添加节点

单击**添加节点**，输入待添加节点的 Host 信息、SSH 端口号、Zone、SSH 用户、认证方式、安装包等，单击**确认**。

关于认证方式的说明如下：

- SSH 密码：输入 SSH 用户对应的密码。

- SSH 密钥：单击**上传**，选择节点的私钥文件。需要提前在待添加节点上生成密钥文件，并将私钥发送给当前电脑（非{{dashboard_ent.name}}机器）。如果设置了短密码（passphrase），也需要填写。

!!! note

    节点添加后，数据不会自动负载均衡。请在[信息总览](../cluster-information/overview-info.md)页面选择图空间执行`Balance Data`和`Balance Leader`操作。

## 节点其他操作

在节点列表中，单击 ![plus](https://docs-cdn.nebula-graph.com.cn/figures/Plus_cn.png) 按钮，查看对应节点的服务名、服务类型、服务状态、运行路径等信息。

- 单击**节点监控**可快速跳转至节点监控页面，详情信息见[集群监控](../2.monitor.md)。

- 单击**服务管理**可快速跳转至服务管理页面。

- 单击**编辑节点**可修改节点设置。

- 当节点上无服务时，可以**删除节点**。删除服务请参见下文**扩缩容**部分。