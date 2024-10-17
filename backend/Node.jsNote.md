# Node.js Note

## 基础知识

### 安装与升级

#### 一、使用 Node.js 官方安装程序

1. 访问 [Node.js官网](https://nodejs.org/zh-cn) 下载对应操作系统的安装程序。
2. 运行安装程序，根据安装向导进行安装。如果已经安装了Node.js，安装程序通常会提供一个"Upgrade"选项，选择这个选项可以自动升级到最新版本。

#### 二、使用 nvm（Node Version Manager）

nvm是一个用于管理多个Node.js版本的便捷工具，特别适用于Unix系统（如Linux或macOS），以及愿意在Windows上使用第三方解决方案的用户。

1. 安装nvm：

   - 对于Unix-like系统（如Linux和macOS），通常通过bash脚本安装。可以访问nvm的GitHub仓库获取安装指令。
   - 对于Windows，可以考虑使用nvm-windows。

2. 使用nvm更新Node.js：

   - 安装最新版本的 Node.js：

     ```bash
     nvm install lts  # lts 代表长期支持版本
     # 如果需要安装最新版本（可能会不稳定），则使用 latest
     nvm install latest
     ```

   - 列出可用的Node.js版本：`nvm list available`。

   - 安装或升级到特定版本：`nvm install <version>`（其中`<version>`是目标版本号）。

3. 使用`nvm use <version>`命令切换到新安装的版本，其中`<version>`是你刚刚安装的Node.js版本号，或者你可以使用`lts`或`latest`作为版本号。

   - 使用新安装的 lts 版本 或 latest

     ```bash
     nvm use lts
     nvm use latest
     ```

   - 使用指定的版本的 Node.js

     ```bash
     nvm use 18.10.1
     ```

   - 可以设置某个版本为默认版本，这样每次打开新的命令窗口时会自动使用这个版本

     ```bash
     nvm alias default lts
     ```

#### 三、使用包管理器（如npm或Yarn）

如果使用的是npm（Node Package Manager）或Yarn等包管理器，它们可能也提供了更新Node.js的功能。以下是使用npm中的n模块来升级Node.js的步骤：

1. 全局安装n模块：`npm install -g n`。
2. 使用n模块升级Node.js：
   - 检查可用版本：`n ls`。
   - 升级到最新稳定版：`n stable`。
   - 升级到最新版：`n latest`。
   - 升级到特定版本：`n <version>`（其中`<version>`是目标版本号）。

#### 四、通过系统包管理器升级（适用于Linux系统）

在某些Linux发行版中，可以通过系统包管理器（如apt、yum或dnf）来升级Node.js。例如：

- 以Ubuntu/Debian为例：`sudo apt update`，然后`sudo apt upgrade nodejs npm`。
- 以Fedora/CentOS为例：`sudo dnf check-update`，然后`sudo dnf upgrade nodejs npm`。

但请注意，系统包管理器提供的版本可能不是最新版本，因此还是建议使用nvm或其他手动安装方法获得最新稳定版Node.js。

#### 五、注意事项

1. 在升级Node.js之前，请确保备份代码和项目，以防万一出现任何问题。
2. 检查项目依赖是否与新版本的Node.js兼容，以避免升级后出现运行错误。
3. 如果不熟悉命令行操作或不确定如何升级，请查阅相关文档或在线资源以获取更多帮助。













