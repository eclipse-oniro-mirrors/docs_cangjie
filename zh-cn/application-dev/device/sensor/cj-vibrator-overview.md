# 振动开发概述

<!--Del-->
> **说明：**
>
> 当前为Beta阶段。
<!--DelEnd-->

通过最大化开放马达器件能力，振动器模块服务拓展了马达服务，实现振动与交互融合设计，打造一体化振动体验和差异化体验，提升用户交互效率和易用性。

## 运作机制

Vibrator属于控制类小器件，包含如下四个模块：Vibrator API、Vibrator Framework、控制类小器件 Service和HDF层。

- Vibrator API：提供振动器的基础API，主要包含振动效果查询、触发/关闭等接口，简化应用开发。
- Vibrator Framework：主要实现振动器框架层管理，实现与控制类小器件Service的通信。
- 控制类小器件 Service：主要实现控制器的服务管理。
- HDF层：适配不同设备。

## 约束与限制

- 要使用振动的功能，设备必须具有对应的器件。
- 使用振动器前需要配置权限`ohos.permission.VIBRATE`，具体配置方式请参见[声明权限](../../security/AccessToken/cj-declare-permissions.md)。
