# CleanerKing

**Windows 全能命令行清理工具 | All-in-one Windows CLI cleanup utility**

---

## Overview / 概述

CleanerKing is a modular Java command-line tool that handles everyday Windows cleanup and maintenance tasks: temp files, browser caches, file search-and-delete, DNS configuration, and quick access to built-in Windows system tools. Built for power users and developers who live in the terminal.

CleanerKing 是一个模块化的 Java 命令行工具，把常见的 Windows 清理维护操作集中在一个控制台里搞定：临时文件清理、浏览器缓存清理、文件搜索删除、DNS 配置、以及 Windows 系统内置工具的快捷调用。面向终端党和开发者，不搞花里胡哨的 GUI，直接干活。

## Features / 功能

Modules registered in `Client.java`, shown in the main menu:

| Module | 功能 | Description |
|--------|------|-------------|
| OneClickCleanModule | 一键清理 | Clears user/system temp, empties Recycle Bin, removes SoftwareDistribution/Prefetch/Recent, wipes Edge/Chrome/Firefox caches, flushes DNS |
| AdvancedCleanModule | 高级清理 | Selective cleanup — choose which targets to hit |
| WindowsToolsModule | Windows 内置工具 | Quick launchers for `cleanmgr`, `diskmgmt.msc`, `msconfig`, `msinfo32`, `dfrgui`, `chkdsk`, `taskmgr`, `resmon` |
| FileSearchModule | 文件搜索与删除 | Search by size, date, keyword, regex — then delete matches |
| DNSModule | DNS 设置 | Inspect network interfaces, configure DNS |
| SettingsModule | 设置 | Toggle logging, loading animation, customize ASCII-art colors |
| ExitModule | 退出 | Confirm and quit |

Console extras: 3D ASCII-art title, loading animation, ANSI color output.

<!-- TODO: Client.java registers option [6] NetworkRepairModule (网络修复模块), but NetworkRepairModule.java doesn't exist yet. Won't compile until added or removed. -->

## Tech Stack / 技术栈

- **Language:** Java (source/target 1.8)
- **Build:** Apache Maven (`org.CleanerKing:CleanerKing:1.0-SNAPSHOT`)
- **Dependencies:**
  - `org.jline:jline` 3.28.0 — terminal interaction
  - `org.slf4j:slf4j-api` + `slf4j-simple` 1.7.36 — logging
  - `junit:junit` 4.13.2 (test)
- **Entry point:** `org.CleanerKing.Client`
- **Platform:** Windows only (uses Windows-specific commands and paths)

## Project Structure / 项目结构

```
CleanerKing/
├── pom.xml
├── LICENSE (MIT)
└── src/main/
    ├── java/org/CleanerKing/
    │   ├── Client.java              # main(), module registration, menu
    │   ├── Utils.java               # cleanup/command/console helpers
    │   ├── Settings.java            # config.properties load/save
    │   ├── ModuleManager/
    │   │   ├── Module.java          # module interface
    │   │   ├── ModuleManager.java   # module registry, menu driver
    │   │   └── Modules/             # OneClickClean, AdvancedClean,
    │   │                            # WindowsTools, FileSearch, DNS,
    │   │                            # Settings, Exit
    │   └── example/                 # AnsiExample, JLineExample (demos)
    └── resources/
        ├── META-INF/MANIFEST.MF
        └── png/img.png
```

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

<!-- TODO: pom.xml 没有 shade/assembly 插件，独立运行 JAR 需要 jLine/SLF4J 在 classpath 上 -->

### Run / 运行

```bat
java -Dfile.encoding=UTF-8 -jar CleanerKing.jar
```

部分清理操作需要管理员权限，建议用管理员终端启动。

Some cleanup actions require Administrator privileges — launch from an elevated terminal.

## Configuration / 配置

`Settings.java` reads/writes `config.properties` in the working directory (auto-created with defaults if missing):

| Key | Default | Description |
|-----|---------|-------------|
| `asciiArtColor` | blue | ANSI color for ASCII-art title / ASCII 标题颜色 |
| `loadingAnimationColor` | green | ANSI color for loading animation / 加载动画颜色 |
| `loggingEnabled` | true | Enable logging / 是否开启日志 |
| `showLoadingAnimation` | true | Show loading animation / 是否显示加载动画 |

## Status / 状态

Personal utility, version `1.0-SNAPSHOT`. Active development — core modules work, `NetworkRepairModule` not yet implemented.

个人工具项目，版本 `1.0-SNAPSHOT`。核心模块可用，`NetworkRepairModule` 还没写完。

## License / 许可证

MIT License. Copyright (c) 2024 dwgx. See [`LICENSE`](LICENSE).

## Contact / 联系

Author: DWGX — dwgx1337@gmail.com
