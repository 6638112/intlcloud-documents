Serverless Framework 支持的 CLI 命令如下：

- **`serverless registry`**：查看可用的 Components 列表。

- **`serverless registry publish`**：发布 Component 到 Serverless 注册中心。

   `--dev`：支持 dev 参数用于发布 `@dev` 版本的 Component，用于开发或测试。

- **`serverless init xxx`**：从注册中心下载指定模版，init 后填入您想下载的模版名称，例 "$ serverless init fullstack"
    
    `sls init xxx --name my-app`：支持自定义项目目录名称

- **`serverless deploy`**：部署 Component 实例到云端。

    `--debug`：列出组件部署过程中 `console.log()` 输出的部署操作和状态等日志信息。

- **`serverless remove`**：从云端移除一个 Component 实例。

    `--debug`：列出组件移除过程中 `console.log()` 输出的移除操作和状态等日志信息。

- **`serverless info`**：获取并展示一个 Component 实例的相关信息。

   `--debug`：列出更多 `state`。

- **`serverless dev`**：启动 DEV MODE 开发者模式，通过检测 Component 的状态变化，自动部署变更信息。同时支持在命令行中实时输出运行日志，调用信息和错误等。此外，支持对 Node.js 应用进行云端调试。

