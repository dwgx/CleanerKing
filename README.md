# CleanerKing

**Windows 命令行全能清理工具 | Modular Windows cleanup CLI in Java**

---

## Overview / 概述

CleanerKing is a modular Java command-line tool that handles everyday Windows cleanup and maintenance: temp files, browser caches, file hunting, DNS config, and quick access to built-in system tools. No bloated GUI, just a console menu for power users and developers who live in the terminal.

CleanerKing 是一个模块化的 Java 命令行工具，把常见的 Windows 清理维护任务集中在一个控制台菜单里：临时文件清理、浏览器缓存清除、文件搜索删除、DNS 配置、以及 Windows 自带工具的快速启动。不搞臃肿图形界面，面向习惯终端操作的高级用户和开发者。

---

## Features / 功能

Modules registered in `Client.java`, shown in the main menu:

| Module | Description |
|--------|-------------|
| **一键清理 / One-click clean** | Clears user/system temp, empties Recycle Bin, removes SoftwareDistribution/Prefetch/Recent, wipes Edge/Chrome/Firefox caches, flushes DNS |
| **高级清理 / Advanced clean** | Selective cleanup — pick which targets to clean |
| **Windows 内置工具 / Built-in tools** | Quick launchers for `cleanmgr`, `diskmgmt.msc`, `msconfig`, `msinfo32`, `dfrgui`, `chkdsk`, `taskmgr`, `resmon` |
| **文件搜索与删除 / File search & delete** | Search by size, date, keyword, regex, then delete matches |
| **DNS 设置 / DNS settings** | Inspect network interfaces, configure DNS servers |
| **设置 / Settings** | Toggle logging/loading animation, customize ASCII-art colors |
| **退出 / Exit** | Confirm and quit |

Console extras: 3D ASCII-art title, loading animation, ANSI color output.

<!-- TODO: Client.java registers NetworkRepairModule (网络修复模块) but no implementation exists yet. Won't compile until the class is added or the registration is removed. -->

---

## Tech Stack / 技术栈

- **Language:** Java (source/target 1.8)
- **Build:** Apache Maven (`org.CleanerKing:CleanerKing:1.0-SNAPSHOT`)
- **Dependencies:**
  - `org.jline:jline` 3.28.0 — terminal interaction
  - `org.slf4j:slf4j-api` + `slf4j-simple` 1.7.36 — logging
  - `junit:junit` 4.13.2 (test)
- **Main class:** `org.CleanerKing.Client`
- **Platform:** Windows only (uses Windows commands and paths)

---

## Project Structure / 项目结构

```
CleanerKing/
├── pom.xml
├── LICENSE (MIT)
├── SECURITY.md
└── src/main/
    ├── java/org/CleanerKing/
    │   ├── Client.java              # main(), module registration, menu
    │   ├── Utils.java               # cleanup/command/console helpers
    │   ├── Settings.java            # config.properties load/save
    │   ├── ModuleManager/
    │   │   ├── Module.java          # module interface
    │   │   ├── ModuleManager.java   # registers modules, drives menu
    │   │   └── Modules/             # OneClickClean, AdvancedClean,
    │   │                            # WindowsTools, FileSearch,
    │   │                            # DNS, Settings, Exit
    │   └── example/                 # AnsiExample, JLineExample (demos)
    └── resources/
        ├── META-INF/MANIFEST.MF
        └── png/img.png
```

---

## Getting Started / 快速开始

### Prerequisites / 前置条件

- JDK 8+
- Apache Maven
- Windows

### Build / 构建

```bash
mvn clean package
```

Produces a JAR under `target/` with `org.CleanerKing.Client` as main class.

<!-- TODO: pom.xml has no shade/assembly plugin, so jLine/SLF4J need to be on classpath for standalone execution. -->

### Run / 运行

```bat
java -Dfile.encoding=UTF-8 -jar CleanerKing.jar
```

部分清理操作需要管理员权限，建议用管理员终端运行。

Some cleanup actions need Administrator privileges — run from an elevated terminal.

---

## Configuration / 配置

`Settings.java` reads/writes `config.properties` in the working directory (auto-created with defaults if missing):

| Key | Default | Description |
|-----|---------|-------------|
| `asciiArtColor` | blue | ANSI color for ASCII-art title |
| `loadingAnimationColor` | green | ANSI color for loading animation |
| `loggingEnabled` | true | Enable/disable logging |
| `showLoadingAnimation` | true | Show/hide loading animation |

---

## Status / 状态

Personal utility, version `1.0-SNAPSHOT`. Active development — core modules work, `NetworkRepairModule` not yet implemented.

个人工具项目，`1.0-SNAPSHOT` 阶段。核心模块可用，`NetworkRepairModule` 还没写完。

---

## License / 许可证

MIT License. Copyright (c) 2024 dwgx. See [`LICENSE`](LICENSE).

---

## Contact / 联系

Author: DWGX — dwgx1337@gmail.com
