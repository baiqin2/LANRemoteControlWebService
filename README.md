 柏钦局域网远控Web神器

#### 介绍
局域网远程控制 Web 服务的 Windows 部署引导程序。
基于 Win32 GDI 自绘界面，支持高 DPI 自适应、多显示器光标反馈、
无边框窗口拖拽与缩放。启动时自动检测本机已部署版本，
未部署则引导用户选择目录完成部署，已部署则提供修复与卸载入口，
全程静默调用系统组件完成服务注册，部署结束自动清理临时文件。
适用于内网无公网环境下的企业内部分发。

#### 软件架构
采用「启动器 + 多子进程」架构，由 SubProcessLauncher 统一拉起：

| 模块 | 作用 |
|---|---|
| LANRemoteControlWebService.exe | 主 Web 后端，提供浏览器控制台 |
| LANFileShareSvc.exe | 文件共享服务（上传 / 下载 / 搜索） |
| BaiqinLANRemoteControlMaster2.exe | 主控端系统托盘 GUI |
| BaiqinDynamicImageLibrary.exe | 屏幕捕获与 JPEG 编码 |
| BaiqinProcessManagement.exe | 进程查看与结束 |
| BaiqinKeyboardLogger.exe | 按键记录（可在设置中关闭） |
| LANRemoteWallpaperServer.exe | 远程壁纸设置 |
| BaiqinMacroRecord.dll | 键鼠宏录制（含音频采样） |
| BaiqinRegeditPage.dll | 远程注册表编辑 |


#### 安装教程

1. 从 从[发行版](https://gitee.com/baiqin1/LANRemoteControlWebService/releases) 下载 “LANRemoteControlWebService.exe”
2. 在被控 Windows 10/11 x64 电脑上双击运行安装包，按提示完成安装
3. 启动「局域网远控神器」，点击「启动服务」
4. 日志出现「服务已启动」后，记下被控机局域网 IP（例如 192.168.1.3）

#### 使用说明

1. 在同一局域网内任意设备浏览器打开 `http://被控机IP:7281/`
2. 首页实时显示被控端屏幕，可直接点页面上的虚拟鼠标 / 键盘操作
3. 文件管理：访问 `http://被控机IP:7283/` 上传、下载或搜索文件
4. 在「运行 EXE」页可远程启动程序，在进程管理页可结束进程
5. 设置页（Settings）可自定义端口、投屏质量、帧率与上传限制

#### 参与贡献

1.  Fork 本仓库
2.  新建 Feat_xxx 分支
3.  提交代码
4.  新建 Pull Request


