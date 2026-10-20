> ### ⚠️ 这是 PCL 的第三方修改版，不是官方版本
>
> - 上游仓库：[Meloong-Git/PCL](https://github.com/Meloong-Git/PCL)，基于 tag `2.99.0.0`（commit `6b9a50d`）。
> - **仅修改**：恢复官方在 2.99.0.0 中移除的「下载 Minecraft」入口。除此之外没有任何代码改动。
> - 本仓库公开该修改的完整源代码，并沿用仓库根目录的 [`LICENCE`](LICENCE)（《PCL 分发有限许可》《PCL 存储库合理使用指南》）。原作者龙腾猫跃保留全部权利；本项目**未获得原作者背书**，若原作者要求将立即停止分发。
> - 完全免费，禁止倒卖或用于任何收费服务。仅供个人学习与技术研究使用。
> - 关于页中的作者署名与赞助链接保持原样未动（`Pages/PageOther/PageOtherAbout.xaml`）。

---

### 这个版本适合怎么用（先看这里）

**一句话：把它当成「MC 下载工具」，日常启动游戏还是用官方 PCL。**

#### 一、它不能在线登录

开源分支没有内置微软登录需要的 Client ID，所以：

- **正版（微软）登录不可用**——点进去也完不成授权，登不上
- 也没有内置 CurseForge 的 API Key，**CurseForge 源的 Mod / 整合包下载会失败**
- 离线登录、第三方认证登录一般还能用，但没有正版皮肤和披风

再加上启动时会弹一次「开源版本说明」，所以它**不适合当日常启动器**。

#### 二、推荐的用法：用它下载，用官方 PCL 启动

| 你要做的事 | 用哪个 |
| --- | --- |
| 下载 Minecraft 版本、装 Forge / Fabric / NeoForge / OptiFine | **本版本** |
| 安装整合包（zip / mrpack） | **本版本** |
| 正版登录、日常启动游戏 | 官方 PCL |
| 检查更新 | 官方 PCL |
| 下载 Mod / 资源包 / 光影（CurseForge 源） | 官方 PCL |

两者用的是**同一个 `.minecraft` 目录**（只要放在同一层文件夹），所以本版本装好的游戏，官方 PCL 打开就能直接看到、直接启动，不需要再挪文件。

#### 三、可以和官方 PCL 的 exe 放在同一个目录

把本版本的 exe 改个名字，和官方 exe 并排放就行：

```text
D:\Games\PCL2\
├─ Plain Craft Launcher 2.exe     ← 官方版：日常登录、启动游戏
├─ PCL 下载专用.exe                ← 本版本：只用来下载
├─ PCL\                           ← 两个版本共用的配置与日志
└─ .minecraft\                    ← 共用的游戏目录
```

要点：

- **exe 可以随便改名**，只要扩展名还是 `.exe`（程序内部的资源是按程序集名加载的，与文件名无关）。
- **共用配置**：两个版本读同一份 `PCL\Setup.ini`，设过的游戏目录、Java、下载源都通用。
- **不能同时开**：PCL 用固定名字做单实例检测（与文件名无关），后启动的那个会“叮”一声、把已开着的窗口叫到前台，然后自己退出。用完一个关掉再开另一个。
- **想完全隔离**：也可以把本版本单独放一个文件夹，再把它里面的「Minecraft 文件夹」指向同一个 `.minecraft`，这样两份配置互不影响。
- 本版本**没有检查更新**，不会自动升级，也不会覆盖官方版的文件。

#### 四、其它差异

- 没有主题切换、没有百宝箱、没有联网通知
- 界面、操作、下载流程与官方版完全一致

---
## 上游 README 原文
# Plain Craft Launcher

[![Stars](https://img.shields.io/github/stars/Meloong-Git/PCL?style=flat&logo=data:image/svg%2bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZlcnNpb249IjEiIHdpZHRoPSIxNiIgaGVpZ2h0PSIxNiI+PHBhdGggZD0iTTggLjI1YS43NS43NSAwIDAgMSAuNjczLjQxOGwxLjg4MiAzLjgxNSA0LjIxLjYxMmEuNzUuNzUgMCAwIDEgLjQxNiAxLjI3OWwtMy4wNDYgMi45Ny43MTkgNC4xOTJhLjc1MS43NTEgMCAwIDEtMS4wODguNzkxTDggMTIuMzQ3bC0zLjc2NiAxLjk4YS43NS43NSAwIDAgMS0xLjA4OC0uNzlsLjcyLTQuMTk0TC44MTggNi4zNzRhLjc1Ljc1IDAgMCAxIC40MTYtMS4yOGw0LjIxLS42MTFMNy4zMjcuNjY4QS43NS43NSAwIDAgMSA4IC4yNVoiIGZpbGw9IiNlYWM1NGYiLz48L3N2Zz4=&logoSize=auto&label=Stars&labelColor=444444&color=eac54f)](https://github.com/Meloong-Git/PCL/)
[![Issues](https://img.shields.io/github/issues/Meloong-Git/PCL?style=flat&label=Issues&labelColor=444444&color=1F883D)](https://github.com/Meloong-Git/PCL/issues)
[![哔哩哔哩](https://img.shields.io/badge/动态-BiliBili-00A4DB?style=flat&labelColor=444444&logoSize=auto)](https://space.bilibili.com/11343203/dynamic)
[![爱发电](https://img.shields.io/badge/赞助-爱发电-946ce6?style=flat&labelColor=444444&logoSize=auto)](https://meloong.com/afd/a/LTCat)

包含 PCL 的大部分源代码，包括 UI 库、动画模块、下载模块、Minecraft 启动模块等！<br/>
代码并不是实时更新的，它会在每次 PCL 发布更新时同步一次。<br/>
非常感谢社区的大力支持！

<br/>

### 相关资源
- [PCL 下载](https://meloong.com/pcl)：下载可免费使用的正式版 PCL！
- [PCL 功能投票](https://github.com/Meloong-Git/PCL/discussions/2)：来参加投票吧，开发者会优先处理票数较高的项目！
- [帮助文档库](https://github.com/LTCatt/PCL2Help)：PCL 内置帮助文档的存储库
