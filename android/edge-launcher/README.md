# 设计目标

在基于 Android 的工业设备上替代默认的 Launcher。其主要改变是，在一般 Launcher 的主要功能（已装应用列表、应用运行、应用关闭、4G信号状态、WI-FI信号状态、时间、电量、消息提醒、短信工具、照片工具）上，增加了授权功能。

授权是指，在交互面板上有一个图标入口，允许进行口令的输入，该功能使用HTTP协议与本地HTTP-Server完成交互。授权通过后，方可执行：系统设置（从隐藏状态变成显示状态）、浏览器（从隐藏状态变成显示状态）、文件夹（从隐藏状态变成显示状态）等。

其主要原则为：在未授权的模式下，只允许使用规定的应用；在授权模式下，允许进行高级别的参数配置。通过授权模式，限制了一般用户对设备的使用范围。包括，应用安装、娱乐等非“工作”功能。

# 软件要求

|指标|参数|描述|
|--|--|--|
| 操作系统 | >= android 6.0 | |
| 屏幕尺寸 | 无要求 | |
| 屏幕方向 | 支持竖屏和横屏 | | 
| 开发语言 | 100% java | |
| 开发框架 | 100% android sdk | |
| 稳定性 | 通过所有测试用例, 包括: 逻辑测试、性能测试、连续使用1个月，无 carsh | |

# 核心功能

| 功能 | 依赖 | 描述 |
|--|--|--|
| 授权 | 无 | 与本地 http-server 交互 |
| 系统设置 | 授权 | 完成授权后显示 |
| 文件管理 | 授权 | 完成授权后显示 |
| 浏览器 | 授权 | 完成授权后显示 |
| OTA | 无 | 与本地 http-server 交互 |
| 照片（相册）管理 | 无 | |
| 短信管理 | 无 | |
| 一般设置 | 无 | 屏幕亮度、方向锁定、截屏 |
| 系统状态显示 | 无 | 蜂窝网络信号、WI-FI信号、蜂窝网络运营商、时间、电量 |
| 服务状态查询 | 无 | 与本地 http-server 交互, 获得服务状态信息并显示 |

# 主要业务流程

- 启动流程

![启动流程](https://raw.githubusercontent.com/UoWakaka/company-public/main/images/img_1.png)

- 运维流程

![运维流程](https://github.com/UoWakaka/company-public/blob/44a85fe7b9d3613b80b0865cc9cb5d00ba117b27/images/img_2.png?raw=true)

# 接口设计

## HTTP接口

- 授权

```
POST http://localhost:5454/v1/edge/core/admin/auth

输入-JSON
{
    "username": "",
    "password": ""
}

http.response.status
| 200 | 成功 |
| x   | 失败 |

输出-JSON
{
    "message": "",
    "code": "http.response.status"
}
```

- 服务状态

```
POST http://localhost:7696/v1/edge/init/state

输入-无

http.response.status
| 200 | 成功 |
| x   | 失败 |

输出-JSON
{
    ...
}
```

# 原型
