# 启动和停止 Pingora 服务器

`Pingora` 服务器是一个常规的非特权多线程进程。

## 启动
默认情况下，服务器将在前台运行。

`Pingora` 服务器默认使用以下命令行参数：

| 参数      | 效果        | 默认值|
| ------------- |-------------| ----|
| -d, --daemon | 后台运行服务器 | false |
| -t, --test | 测试服务器配置然后退出 (WIP) | false |
| -c, --conf | 配置文件的路径 | 空字符串 |
| -u, --upgrade | 此服务器应优雅地升级运行中的服务器 | false |

## 停止
`Pingora` 服务器将监听以下信号。

### SIGINT：快速关闭
收到 `SIGINT` 信号 `(ctrl + c)` 后，服务器将立即退出，没有延迟。所有未完成的请求将被中断。这种行为通常不太受欢迎，因为它可能中断请求。

### SIGTERM：优雅关闭
收到 `SIGTERM` 信号后，服务器将通知所有服务关闭，等待一段预先配置的时间，然后退出。这种行为为请求提供了一个优雅结束的时间。

### SIGQUIT：优雅升级
类似于 `SIGTERM`，但服务器还将所有监听的`Socket`传输到新的 `Pingora` 服务器，以确保在升级期间没有停机。有关详细信息，请参阅[优雅升级](graceful.md)部分。
