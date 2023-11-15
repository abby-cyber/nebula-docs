# 内联框架

{{explorer.name}}支持内联框架（iframe），可以将画布嵌入至第三方页面中使用。本文介绍如何嵌入画布。

## 前提条件

已安装{{explorer.name}}。

## 注意事项

- 嵌入的{{explorer.name}}页面默认直接访问目标图空间，因此会屏蔽部分页面及功能。例如上方导航栏、左侧导航栏中的模板查询和切换图空间等。如果需要访问多个图空间，可以在多个页面中分别嵌入。
- 暂不支持切换语言，默认为中文页面。

## 步骤

1. 在{{explorer.name}}安装目录内修改配置文件`config/app-config.yaml`。需要修改的内容如下。

  ```bash
  # 取消 CertFile 和 KeyFile 参数的注释。
  CertFile: "./config/NebulaGraphExplorer.crt"
  KeyFile: "./config/NebulaGraphExplorer.key"

  # 修改 IframeMode.Enable为 true。
  IframeMode:
    Enable: true
  # 可以设置窗口的 URI 白名单，默认无限制。
    # Origins:
    #  - "http://192.168.8.8"
  ```

2. 在`config`文件夹内使用`openssl`命令生成自签名证书。示例如下。

  ```bash
  openssl req -newkey rsa:4096 -x509 -sha512 -days 365 -nodes -subj "/CN=NebulaGraphExplorer.com" -out NebulaGraphExplorer.crt -keyout NebulaGraphExplorer.key
  ```

  - `-newkey`：生成证书请求或者自签名证书的时候自动生成密钥。
  - `-x509`：生成自签名证书。
  - `-sha512`：指定消息摘要算法。
  - `-days`：`-x509`生成的证书的有效天数。
  - `-nodes`：不加密输出密钥。
  - `-subj`：设置请求的主题。
  - `-out`：指定生成的证书请求或者自签名证书名称。
  - `-keyout`：指定自动生成的密钥名称。

3. 用户自行开发，在第三方页面中通过 iframe 方式嵌入{{explorer.name}}。

4. 在父页面通过 postMessage 方法传递请求，示例如下：

  ```json
  const links = [
    {
      source: 'player150',
      target: 'player143',
      id: 'follow player150->player143 @0',
      rank: 0,
      edgeType: 'follow',
      properties: {
        degree: 90,
      },
      color: '#d40e0e',
    },
    {
      source: 'player143',
      target: 'player150',
      id: 'follow player143->player150 @0',
      rank: 0,
      edgeType: 'follow',
      properties: {
        degree: 90,
      },
    },
  ];

  const nodes = [
    {
      id: 'player150',
      tags: ['player'],
      properties: {
        player: {
          age: 20,
          name: 'Luka Doncic',
        },
      },
      color: '#20eb14',
    },
    {
      id: 'player143',
      tags: ['player'],
      properties: {
        player: {
          age: 23,
          name: 'Kristaps Porzingis',
        },
      },
      color: '#3713ed',
    },
  ];

  // 登录
  iframeEle.contentWindow.postMessage(
    {
      // `NebulaGraphExploreLogin` 类型已经弃用，使用 `ExplorerLogin` 代替，但是在 3.x 版本中继续保持兼容。
      type: 'ExplorerLogin',
      data: {
        authorization: 'WyJyb290IiwibmVidWxhIl0=',  //{{nebula.name}}账号和密码组成数组并序列化，然后进行 Base64 编码。数组格式为`['账号', '密码']`，示例为`['root', 'nebula']`，编码后为`WyJyb290IiwibmVidWxhIl0=`。
        host: '192.168.8.240:9669',  //{{nebula.name}}的 Graph 服务地址。
        space: 'demo_basketball',  //目标图空间名称。
      },
    },
    '*'
  );

  // 画布添加点边
  iframeEle.contentWindow.postMessage({ type: 'ExplorerAddCanvasElements', data: { nodes, links } }, '*')

  // 清空画布
  iframeEle.contentWindow.postMessage({ type: 'ExplorerClearCanvas' }, '*')
  ```

5. 启动{{explorer.name}}服务。

  !!! note

        如果是 RPM/DEB 安装的{{explorer.name}}，请执行命令`sudo ./yueshu-explorer-server &`。

  ```bash
  ./scripts/start.sh
  ```

6. 访问第三方页面，检查是否可以查看到嵌入的{{explorer.name}}页面。示例页面中第一个页面展示`basketballplayer`图空间，第二个和第三个页面展示其他图空间。

  ![iframe_example](https://docs-cdn.nebula-graph.com.cn/figures/explorer_iframe_example_221025.png)