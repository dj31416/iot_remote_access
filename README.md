# 阿里云IoT远程运维套装之远程访问设备端源码

## 功能

* 跨公网SSH到你的设备上，并提供基于浏览器方案的免安装web shell.
* 无需公网IP，直接浏览设备上的文件，并提供下载/上传功能.
* 内网穿透，支持跨公网访问Windows远程桌面.
* Android ADB不再局限于局域网调试.
* 免费，开源，稳定，安全的远程运维神器。
* 更多介绍，请浏览 [WIKI](https://github.com/alibaba/iot_remote_access/wiki)
## 编译

以下在ubuntu上演示如何编译。
### 下载Scons

```shell
sudo apt-get install -y scons
```

### 编译

```shell
scons
```

### 生成物介绍

```
RemoteTerminalDaemon: 动态链接库版本的可执行程序，运行需要将nopoll和openssl库放到系统库里或者手动指定LD_LIBRARY_PATH.
RemoteTerminalDaemon_static: 静态库链接版本的可执行程序，可直接运行. 
```

## 运行
两种运行方式的差异在于设备三元组在配置文件里面传递还是通过命令行参数传递。
### 配置文件方式

* 配置文件说明

```shell
{
	"cloud_ip": "backend-iotx-remote-debug.aliyun.com",       //连接云端的ip或者url，无需修改。
	"cloud_port": "443",              //连接云端的端口，无需修改。
	"cert_path": "root.pem",            //TSL握手需要的根证书存储路径，无需修改。
	"is_tls_on": 1,                     //是否支持TLS，默认为1，无需修改。
	"is_debug_on": 0,                   //是否打开调试模式，可以填0或者1，调试模式下，有更丰富的打印信息.
	"listen_port": 22,                  //监听本地的端口号，一般为需要代理的服务端口号，比如SSH为22，telnet为21，ftp为23等。
	"listen_ip": "127.0.0.1",           //监听代理服务的IP号，一般为localhost的IP地址.
	"product_key": "aaaaaaaaaaa",       //阿里云IoT物联网平台上的ProductKey，具体请参考: https://help.aliyun.com/document_detail/73729.html?spm=a2c4g.11174283.6.584.5fd91668DmxBzt 
	"device_name": "bbbbbbbbbbbbb",     //阿里云IoT物联网平台上的DeviceName
	"device_secret": "cccccccccccccccccccccccccccccccc"   //阿里云IoT物联网平台上的DeviceSecret
}

```
* 修改配置文件里的product_key, device_name, device_secret三项.

* 运行

```shell
./RemoteTerminalDaemon_static
```

### 命令行方式 
```shell
./RemoteTerminalDaemon_static ProductKey DeviceName DeviceSecret

直接运行，后面跟上设备三要素即可。
```

**注意**: 必须把board/xxx/prebuilt下面所有的.so，顶层目录的root.pem，顶层目录的remote_terminal.json及RemoteTerminalDaemon同时安装在设备上
才能运行成功。

PS: 如有任何问题，请钉钉扫描咨询。
![asdf](https://camo.githubusercontent.com/bc61a578aa686d36c550ee657498786a0afdffdf/68747470733a2f2f63646e2e6e6c61726b2e636f6d2f6c61726b2f302f323031382f706e672f31363035352f313534333838383432313239332d36643638663830632d376261362d343363362d383737372d6331636365623035643834642e706e67)
