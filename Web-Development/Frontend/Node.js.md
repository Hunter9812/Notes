[微软官方 Node.js 入门教程](https://www.bilibili.com/video/BV1kN41197vw/)
# 安装

由于权限和更新问题，我们需要下一个NVM（Node Version Manager）

- [nvm](https://github.com/nvm-sh/nvm)：mac、linux
- [nvm-windows](https://github.com/coreybutler/nvm-windows)：windows

常用命令

- `nvm list avaliable`
- `nvm install 12.18.2`
- `nvm use 16.18.1`

# npm(Node Package Manager)
> yarn、pnpm是npm的替代品

- `npm init`
  初始化你的package.json

- `npm install`
  安装当前项目的所有依赖项

  - -g
    将包全局安装

  - --save-dev
    -D
    将包添加到项目的开发依赖中。

    > 开发依赖是指在开发过程中需要使用的包，而不是在生产环境中需要使用的包。

  - --save
    -S
    将包作为生产依赖项安装

- `npm uninstall`
  卸载依赖项

- `npm run start（script）`
  运行脚本

- 更新

  - `npm outdated`
    列出过期的包
    - 黄色：现有最新版本，但版本不在package.json文件的可更新范围内。
      如何更新：`npm install express@latest`
    - 红色：在package.json指定范围内（可以更新）
  - `npm update`
    更新所有红色的包
    vscode的Version Lens拓展可以更新（如果不想使用命令行）

- 管理漏洞

  - `npm audit`
    列出漏洞的种类信息、哪些包受到影响以及如何解决
  - `npm audit fix`
    尝试通过更新在可用版本范围的包来解决问题
    - `npm audit fix --force`
      允许版本范围之外的更新，meaning 主版本更新

# nodejs

- package.json

  ```json
  "scripts": {
          "start": "node ./dist/index.js",
          "test": "jest",
          "build": "tsc",
          "lint": "eslint"
  },
  "dependencies": {
          "express": "^4.18.2"
  },
  ```

  - 包的版本号

    - [语义化版本](https://semver.org/lang/zh-CN/)(semantic versioning)的行业标准

      > 版本格式：主版本号.次版本号.修订号，版本号递增规则如下：
      >
      > 1. 主版本号：当你做了不兼容的 API 修改，（你要改代码）
      > 2. 次版本号：当你做了向下兼容的功能性新增，（添加新功能）
      > 3. 修订号：当你做了向下兼容的问题修正。（补丁）
      >
      > 先行版本号及版本编译信息可以加到“主版本号.次版本号.修订号”的后面，作为延伸。

    - 特殊字符

      三个特殊字符表示可更新范围

      - `^`脱字符

        当你使用npm install package表示允许中号和小号版本更新，禁止大号更新

      - `~`波浪号

        会限制仅更新小号，对关键包很有用（e.g.编译器 or Linter）

      - 只有版本号

        不会更新

      - 将主版本号改为`*`

        总会更新到最新版本





