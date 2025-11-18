---
title: Hexo 搭建系列（一）：基础搭建
tags: [Hexo, 博客搭建]
categories: [Hexo 博客搭建系列]
topic: hexo # 专栏
banner: /blog/assets/images/hexo.png
author: Humphrey
references: 
  - '[Hexo官方文档](https://hexo.io/zh-cn/docs/)'
date: 2025-11-14 16:09:11
description: 个人博客搭建系列第一篇，记录 Hexo 基础环境准备与初始搭建步骤，为后续主题配置、部署上线做铺垫，方便自己回顾和系列内容衔接。
---

> __Description:__
> 个人博客搭建系列第一篇，记录 Hexo 基础环境准备与初始搭建步骤，为后续主题配置、部署上线做铺垫，方便自己回顾和系列内容衔接。

## 前言

> Hello 大家好呀！最近好多小伙伴问我个人博客是怎么搭建的，想着干脆开一个系列专栏，从 0 到 1 手把手教大家用 Hexo 搭建属于自己的专属博客。这是系列的第一篇，核心聚焦「基础环境准备」和「初始搭建」这两个关键环节——毕竟万丈高楼平地起，把基础打牢了，后续的主题美化、插件配置、部署上线才能顺风顺水。话不多说，咱们直接开干！

## 一、环境准备

Hexo 运行依赖 {% mark Node.js %} 和 {% mark Git %} 两个核心工具，前者是运行 Hexo 的 JavaScript 运行环境，后者用于版本控制和后续部署到代码托管平台。下面分步骤讲清楚不同系统的安装方法，Windows、Mac（含 M 芯片和 Intel 芯片）的同学都能找到对应方案。

### 安装 Node.js（推荐用 NVM 管理）

{% note 为什么推荐用&nbsp;NVM（Node&nbsp;Version&nbsp;Manager）？ 因为不同项目可能依赖不同版本的 Node.js，直接安装 Node 会出现版本冲突问题，而 NVM 能轻松切换多个 Node 版本，简直是开发者的福音。 %}

#### 安装 NVM

##### Windows 电脑安装方法

1. __下载安装包__
  > 打开 [NVM for Windows 官方仓库](https://github.com/coreybutler/nvm-windows/releases)，下载最新版本的 `nvm-setup.exe` 安装包（一般是列表里第一个带 **Setup** 字样的文件）。

2. __执行安装__
  > 双击安装包，第一步同意协议后点击「Next」；第二步选择 NVM 安装路径（建议默认，比如 `C:\Program Files\nvm`，记住路径后续可能用到）；第三步选择 Node.js _symlink 路径（默认即可）；最后点击「Install」完成安装。

3. __验证安装__
  > 按下 {% kbd Win %} + {% kbd R %}输入 `cmd` 打开命令提示符，输入 `nvm version`。如果输出类似 `1.1.11` 的版本号，说明安装成功；如果提示「不是内部或外部命令」，重启电脑再试（若仍失败，检查安装时路径是否有空格或中文，重新安装到纯英文无空格路径）。

##### Mac 电脑安装方法

Mac 安装 NVM 推荐用终端命令行，M 芯片和 Intel 芯片的核心步骤一致，仅部分权限细节有差异，下面分别说明。

###### M 芯片（Apple Silicon）安装方法

1. __打开终端__
  > 通过「启动台 → 其他 → 终端」打开，或按下 `Command + 空格` 输入 `终端` 打开。

2. **执行安装命令**：
  > 输入以下命令并回车（这是 NVM 官方推荐的安装脚本）：

    ```shell
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
    ```

    {% note Tips: 如果提示 `curl: (7) Failed to connect to raw.githubusercontent.com port 443: Connection refused`，说明网络有墙，可切换手机热点再试，或用国内镜像脚本： %}

    ```shell
    `curl -o- https://gitee.com/mirrors/nvm/raw/master/install.sh | bash`
     ```

3. **配置环境变量**：
  > 1. 安装完成后，终端会提示`Close and reopen your terminal`
  > 2. 先关闭终端再重新打开；若重新打开后输入 `nvm --version` 仍提示命令不存在，需手动配置环境变量：
  > 3. 输入 `open ~/.zshrc`（M 芯片 Mac 默认shell是zsh），在打开的文件末尾添加以下内容：
    ```
    export NVM_DIR="$HOME/.nvm"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
    [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
    ```
  > 4. 保存文件后，回到终端输入 `source ~/.zshrc` 使配置生效。

4. **验证安装**：
  > 输入 `nvm --version`，输出类似 `0.40.1` 的版本号即成功。

###### Intel 芯片安装方法

1. **打开终端**：
  > 同 M 芯片步骤1。

2. **执行安装命令**：
  > 和 M 芯片步骤2一致，输入官方脚本或国内镜像脚本。

3. **配置环境变量**：
  > Intel 芯片老版本 Mac 可能用 bash shell，若 `open ~/.zshrc` 提示文件不存在，输入 `open ~/.bash_profile`，添加和 M 芯片相同的环境变量内容，保存后输入 `source ~/.bash_profile` 生效。

4. **验证安装**：
  > 同 M 芯片步骤4，输出版本号即成功。

#### 使用 NVM 安装 Node.js（22 版本）

不管是 Windows 还是 Mac，安装完 NVM 后，安装 Node.js 的步骤都一致，咱们统一操作：

1. **安装指定版本**：
  > 打开终端/命令提示符，输入 `nvm install 22` 并回车。
  > NVM 会自动下载并安装 Node.js 22 版本（包含对应版本的 npm，npm 是 Node.js 的包管理工具）。
  
    ```
    小贴士:
    如果下载速度慢
    Windows:
    可修改 NVM 安装目录下的 `settings.txt` 文件，添加两行镜像配置：
    node_mirror: https://npm.taobao.org/mirrors/node/
    npm_mirror: https://npm.taobao.org/mirrors/npm/
    Mac:
    可在终端输入 `nvm install 22 --registry=https://registry.npm.taobao.org` 用国内镜像加速。
    ```

2. **切换到已安装版本**：
  > 输入 `nvm use 22` 并回车。
  > Windows 可能需要以管理员身份打开命令提示符才能切换成功（右键命令提示符 → 以管理员身份运行）。

3. **设置默认版本（可选但推荐）**：
  > 为了避免每次打开终端都要重新切换版本，
  > Windows 输入 `nvm alias default 22`，
  > Mac 输入 `nvm alias default 22`，将 22 版本设为默认。

#### 校验 Node.js 安装是否完成

> 在终端/命令提示符中输入两个命令验证：

1. `node -v`：输出类似 `v22.6.0` 的版本号，说明 Node.js 安装成功。

2. `npm -v`：输出类似 `10.8.1` 的版本号，说明 npm 安装成功。

### 安装 Git

Git 是分布式版本控制系统，后续 Hexo 部署到 GitHub、Gitee 等平台时需要用到，同时本地管理博客源码也很方便。同样分系统说明：

#### Windows 电脑安装方法

1. **下载安装包**：
  > 打开[ Git 官方下载页](https://git-scm.com/download/win)，页面会自动识别系统版本并提供 32 位/64 位安装包，点击下载即可。

2. **执行安装**：
  > 双击安装包，大部分步骤默认下一步即可，关键步骤提醒：
    - 选择安装路径：建议纯英文无空格，比如 `C:\Program Files\Git`；
    - 选择编辑器：默认 Vim 即可，新手也可选 Notepad++；
    - 调整环境变量：选择「Use Git from Git Bash only」或「Use Git from the Windows Command Prompt」（推荐后者，可在命令提示符和 Git Bash 中都使用 Git）；
    - 换行符转换：选择「Checkout as-is, commit Unix-style line endings」（避免跨系统协作时换行符问题）；
    - 终端模拟器：默认「Use MinTTY」即可。
    最后点击「Install」完成安装。

3. **验证安装**：
  > 打开命令提示符或 Git Bash，输入 `git --version`，输出类似 `git version 2.45.1.windows.1` 的版本号即成功。

#### Mac 电脑安装方法

##### M 芯片安装方法

> 推荐用 Homebrew 安装（Homebrew 是 Mac 上的包管理器，后续装其他工具也方便）：

1. **安装 Homebrew（若未安装）**：
  > 打开终端，输入官方脚本并回车：
    ```
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"   
    ```
  > 安装过程中会提示输入密码（Mac 登录密码），输入时不会显示字符，输完回车即可；
  > 若网络问题失败，可改用国内镜像脚本（自行搜索「Homebrew 国内安装脚本」）。

2. **用 Homebrew 安装 Git**：
  > 输入 `brew install git` 并回车，Homebrew 会自动下载安装最新版本的 Git。

3. **验证安装**：
  > 输入 `git --version`，输出类似 `git version 2.45.1` 的版本号即成功。

##### Intel 芯片安装方法

> 两种方式可选，推荐 Homebrew 安装，步骤和 M 芯片完全一致；若不想装 Homebrew，可直接下载官方安装包：

1. 打开 Git 官方下载页（[https://git-scm.com/download/mac](https://git-scm.com/download/mac)），下载对应 Intel 芯片的 .dmg 安装包；

2. 双击安装包，按照提示拖到应用程序文件夹即可完成安装；

3. 验证方法同 M 芯片，输入 `git --version` 查看版本。

#### 常见错误解决方法

- **错误1：Git 安装后提示「不是内部或外部命令」**：
  > 原因是环境变量未配置，
  > Windows 可右键「此电脑」→「属性」→「高级系统设置」→「环境变量」，在「系统变量」的「Path」中添加 Git 的 bin 路径（比如 `C:\Program Files\Git\bin`），保存后重启终端；
  > Mac 一般不会出现此问题，若出现可输入 `export PATH=/usr/local/bin:$PATH` 临时配置。

- **错误2：Mac 安装 Git 时提示「权限不足」**：
  > 在安装命令前加 `sudo`，比如 `sudo brew install git`，输入密码后执行（sudo 表示以管理员权限运行）。

- **错误3：Git 版本过低**：
  > Windows 可卸载旧版本后重新下载最新安装包；
  > Mac 用 Homebrew 安装的可输入 `brew upgrade git` 升级。

## 二、安装 Hexo

Node.js 和 Git 都准备好后，安装 Hexo 就非常简单了，通过 npm 全局安装即可，一步到位：

### 全局安装并校验

1. **执行安装命令**：
  > 打开终端/命令提示符，输入以下命令并回车：
  >  
    ```shell
    npm install -g hexo-cli

    # -g 表示全局安装，这样在任何目录下都能使用 hexo 命令；
    ```
  > 若下载速度慢，可先配置 npm 国内镜像：
    ```shell
    npm config set registry https://registry.npm.taobao.org
    ```
配置完成后再执行安装命令。

2. **校验安装成功与否**：
  > 输入 `hexo -v` 并回车，若输出类似以下的版本信息，说明安装成功：
    ```
    hexo-cli: 4.3.0
    os: win32 10.0.19045
    node: 22.6.0
    v8: 12.4.254.26-node.26
    uv: 1.48.0
    zlib: 1.3.1
    brotli: 1.1.0
    ares: 1.27.0
    modules: 128
    nghttp2: 1.62.1
    napi: 9
    llhttp: 9.1.3
    uvwasi: 0.0.19
    acorn: 8.12.1
    simdutf: 4.0.8
    cldr: 45.1
    icu: 75.1
    tz: 2024a
    unicode: 15.1
    ngtcp2: 1.2.1
    nghttp3: 1.1.0
    ```

  {% note 常见错误：若提示「npm&nbsp;ERR!&nbsp;Permission&nbsp;denied」（权限不足） Windows 以管理员身份打开命令提示符；Mac 在命令前加 `sudo`，即 `sudo npm install -g hexo-cli`。 %}

## 三、初始化 Hexo 项目

Hexo 安装完成后，就可以初始化一个博客项目了，这一步会生成博客的基础目录结构和默认配置。

### 执行初始化命令

1. **选择项目目录**：
  > 先在电脑上新建一个文件夹作为博客根目录（比如 `D:\MyBlog` 或 `~/MyBlog`），然后在终端/命令提示符中进入该目录：
  > Windows：`cd D:\MyBlog`
  > Mac：`cd ~/MyBlog`

2. **初始化项目**：
  > 输入 `hexo init` 并回车。
  > Hexo 会自动下载博客所需的基础文件和依赖包，这个过程需要一点时间，耐心等待即可。

  {% note 小贴士： 若提示「hexo init 命令不存在」，先检查 hexo 是否安装成功（`hexo -v`），若未成功重新安装；若已成功，Windows 重启命令提示符，Mac 重启终端再试。 %}

3. **安装依赖（若初始化时未自动安装）**：
  > 少数情况下初始化后依赖未安装完整，可手动输入 `npm install` 安装依赖。

4. **启动本地预览**：
  > 输入 `hexo s`（s 是 server 的缩写）并回车，启动本地服务器。
  > 待终端提示
  > ```
    Hexo is running at http://localhost:4000
    Press Ctrl+C to stop.
    ```
  > 打开浏览器输入 `http://localhost:4000`，就能看到 Hexo 的默认博客页面了！是不是很有成就感？

### 3.2 Hexo 项目目录讲解

初始化完成后，博客根目录会生成以下文件夹和文件，理解这些目录的作用对后续配置至关重要，咱们逐个说明核心目录：

```
├── _config.yml # 网站的 配置 文件。 您可以在此配置大部分的参数。
├── package.json # 项目依赖配置文件，记录了项目的依赖包信息和脚本命令。
├── scaffolds # 模版 文件夹。 当您新建文章时，Hexo 会根据 scaffold 来创建文件。
├── source
|   ├── _drafts  # 存放草稿文章，默认没有，可手动新建；
|   └── _posts   # 存放博客文章，格式为 Markdown 文件（.md），后续写的文章都放这里；
└── themes  # 主题 文件夹。 Hexo 会根据主题来生成静态页面。
```

### 3.3 常用命令讲解

Hexo 的操作主要通过命令行完成，掌握以下几个常用命令，日常管理博客基本够用：

|命令|缩写|作用说明|使用场景|
|---|---|---|---|
|hexo init [文件夹名]|无|初始化 Hexo 项目，若指定文件夹名则新建该文件夹并初始化，不指定则在当前目录初始化|首次创建博客项目|
|hexo new [文章标题]|hexo n|在 source/_posts 下新建一篇 Markdown 格式的文章，文件名会自动加上日期|写新文章时使用|
|hexo generate|hexo g|将源文件生成静态网页文件，存放在 public 目录下|部署前必须执行，生成可部署的静态文件|
|hexo server|hexo s|启动本地开发服务器，默认地址 http://localhost:4000，可实时预览博客效果|写文章或修改配置后，预览效果|
|hexo clean|无|清除 public 目录和缓存文件（db.json）|修改主题或配置后预览异常时，先执行 clean 再 g 和 s|
|hexo deploy|hexo d|将 public 目录的静态文件部署到配置的服务器（如 GitHub）|生成静态文件后，部署到线上让别人访问|



 {% note 小贴士 命令可以组合使用，比如 `hexo clean && hexo g && hexo s`，表示先清除缓存，再生成静态文件，最后启动本地服务器，一步到位。 %}

# 四、结尾

 {% note 到这里,&nbsp;Hexo&nbsp;博客的基础搭建就完成啦！ 咱们回顾一下：从安装 NVM 管理 Node.js，到安装 Git 做版本控制，再到安装 Hexo 并初始化项目，最后通过本地预览看到了第一个默认博客页面。整个过程虽然涉及多个工具的安装，但只要跟着步骤一步步来，应该都能顺利完成。 %}

> 基础搭建完成后，后续的内容就更有意思了——下一篇咱们会讲「Hexo 主题配置」，教大家如何更换心仪的主题、修改主题样式，让你的博客从默认样式变得独一无二；再之后还会讲插件安装、博客部署上线等内容，让你的博客真正能被全世界访问。

<!-- 如果在搭建过程中遇到问题，欢迎在评论区留言，也可以参考文末的 Hexo 官方文档查资料。咱们下一篇再见，祝大家都能搭建出自己满意的博客！ -->
