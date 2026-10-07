# 番茄净化

[官网](https://fanqie.goforit.si/) · [插件源](https://apt.mjh.im) · [下载 3.0.3](https://github.com/5hux1n/fanqiefn/releases/tag/v3.0.3)

iOS 越狱插件，为番茄小说（com.dragon.read）提供广告与界面净化、通知/小组件伪装、会员状态伪装，并在原生设置菜单加入“番茄净化”二级菜单入口。

## 3.0.3

- 新增书城和我的页发帖悬浮按钮的独立隐藏开关。
- 新增短剧导航隐藏与关闭进入自动播放开关，保留手动播放。

新增控制首次默认关闭，沿用原生二级设置与总开关，保留已有配置。

- 屏蔽阅读页广告插入、底部广告、章末广告/小游戏/直播/优惠券推广卡。
- 屏蔽听书信息流广告、小游戏入口，以及个人页部分直播、商城和关注推荐入口。
- 隐藏最新章节下方的圈子帖子卡片，保留催更和更新日历；章末圈子按钮有独立开关。
- 关闭自动书籍评价邀请，保留手动评价与评论。
- 隐藏原生/KMP 听读赚钱福利挂件及引导气泡。
- 保留章末容器、催更和更新日历。安装测试前请卸载旧图层插件。
- 保留原有通知与小组件权限伪装；修正通知授权 Hook 的实例方法声明及初始化入口。

会员状态伪装默认开启，到期时间设为北京时间 9999-12-31 23:59:59；这不修改服务端订阅或保证付费内容可用。全局 AVPlayer、头像签名验证和环境检测改动没有移植。

原生“插件总开关”可暂停全部功能及启动页覆盖，保留各分项选择。设置底部显示 3.0.3，并提供作者 GitHub 与插件源入口。更新日志见 [Releases](https://github.com/5hux1n/fanqiefn/releases)。

## 原生设置开关

进入“我的 → 设置”，第一个分区中“清理缓存”上方的“番茄净化”进入二级设置页。入口、分区、菜单行和开关均复用番茄自身的 `SSSettingViewController`、`SSSettingTableViewCell` 和 `SSMaterialSwitch`，没有自绘单元格或滚动保存提示。

共 **插件总开关 + 23 个功能开关 + 默认启动页菜单 + 底部版本/作者/源链接分区**：

- 插件总开关：位于二级菜单第一行，默认开启；关闭后暂停所有功能及启动页覆盖，保留各分项选择和设置入口。

- 原有九项净化/伪装功能。
- 章末作者的话、本章讨论、圈子按钮、送礼物、最新章节三个按钮：各自独立，首次默认关闭；开启后隐藏。
- 底部福利导航、我的页面福利卡片：首次默认隐藏整张金币/余额/提现卡片；保留下方圈子及其他模块。
- 我的页关注推荐卡片：独立隐藏开关，首次默认关闭，保留卡片。
- 返回按钮标题固定为当前章节名：首次默认开启，翻章后跟随当前页面更新。
- 允许快速跳过激励广告：首次默认关闭；开启后使用现有关闭按钮直接执行 SDK 原生关闭流程，跳过退出确认。不伪造奖励到账或完成观看状态；目前覆盖内置 BDA 激励广告页面。
- 默认启动页：书城 / 短剧 / 书架 / 我的 / 跟随 App 设置，复用番茄的原生选择面板。默认跟随 App，不影响原设置；选择其他项后冷启动按所选页面进入。

会员到期仍为 9999-12-31，原有保存值保留。阅读右上角金币倒计时/“去赚更多”按用户要求不再增加插件开关，沿用 App 自带设置。开关保存在本机；切换后彻底结束并重新打开番茄，使已生成的页面和底部导航重新加载。催更、更新历史仍保留。

## 功能

- **通知权限伪装** — 拦截 iOS 通知授权请求，始终返回已授权，避免弹出系统通知权限对话框
- **通知设置伪装** — 将所有通知设置（提示、声音、角标、预览）伪装为已启用状态
- **远程推送伪装** — 返回已注册远程推送状态，拦截注册调用避免触发弹窗
- **小组件伪装** — 拦截 `NSUserDefaults` 中小组件相关 key 的读取，返回已添加状态
- **弹窗拦截** — 拦截包含小组件关键词的 `UIAlertController` 弹窗，彻底去除提醒

## 安装

### 系统要求

- iOS 15.0+
- Rootless（Dopamine / palera1n）或 RootHide 越狱环境
- 番茄小说已安装

### 方式一：下载预编译包

在 Sileo / Irisin 添加 `https://apt.mjh.im`，搜索“番茄净化”；或从 [官网](https://fanqie.goforit.si/#download) 选择适合的方案。

| 方案 | 安装包 | 安装布局 |
|---|---|---|
| Rootless | `fanqiefn_3.0.3_iphoneos-arm64.deb` | `/var/jb/Library/MobileSubstrate/DynamicLibraries` |
| RootHide | `fanqiefn.roothide_3.0.3_iphoneos-arm64e.deb` | `/Library/MobileSubstrate/DynamicLibraries` |

两种包均含 arm64 与 arm64e 切片；RootHide 原生构建，不能仅改 Rootless 包的 Architecture。对应 dylib 与 SHA256SUMS 同时提供。

从 [Releases](https://github.com/5hux1n/fanqiefn/releases) 页面下载 `.deb` 文件，使用包管理器（Sileo / Irisin）安装，或通过命令行：

```bash
dpkg -i fanqiefn_*.deb
```

## 免责声明

本项目仅供学习和研究使用，请勿用于任何违反法律法规或番茄小说用户协议的用途。使用本插件所产生的任何后果由使用者自行承担。

## 直接下载 v3.0.3

- [fanqiefn.roothide_3.0.3.dylib](https://github.com/5hux1n/fanqiefn/releases/download/v3.0.3/fanqiefn.roothide_3.0.3.dylib)
- [fanqiefn.roothide_3.0.3_iphoneos-arm64e.deb](https://github.com/5hux1n/fanqiefn/releases/download/v3.0.3/fanqiefn.roothide_3.0.3_iphoneos-arm64e.deb)
- [fanqiefn_3.0.3.dylib](https://github.com/5hux1n/fanqiefn/releases/download/v3.0.3/fanqiefn_3.0.3.dylib)
- [fanqiefn_3.0.3_iphoneos-arm64.deb](https://github.com/5hux1n/fanqiefn/releases/download/v3.0.3/fanqiefn_3.0.3_iphoneos-arm64.deb)
- [SHA256SUMS](https://github.com/5hux1n/fanqiefn/releases/download/v3.0.3/SHA256SUMS)

[历史版本下载](https://github.com/5hux1n/fanqiefn/releases)
