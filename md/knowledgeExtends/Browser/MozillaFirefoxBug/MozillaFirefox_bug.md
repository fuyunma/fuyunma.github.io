
##更新火狐49.0.2后Flash出现问题的解决方法
Q：
uploadify 上传控件，在更新 49.0.2 版本的 Firefox 之后变的不透明
Flash页游占用内存过高
B站等一系列使用 Flash 播放的网站全屏后出现问题

A：
Firefox 49.0.2 版本的更新中默认启用了 Flash 插件的异步呈现 Bug 1307108。 这可以提高使用 Flash 插件的网站的性能并减少崩溃。但在不同硬件环境下（主要是x64_86）Flash 又会出现一系列新问题 Bug 1305135 Bug 1312043

出现了此类问题，建议先将Flash更新至最新版本，看问题是否还会出现。如果问题依然存在，可以先将Flash插件的异步呈现关闭：

#####地址栏输入 about:config 搜索 dom.ipc.plugins.asyncdrawing.enabled，双击将值改为 false
#####重启浏览器