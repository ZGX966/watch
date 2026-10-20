# STM32 智能手表（STM32-WATCH）

基于 **STM32F103** + **Keil MDK** 的智能手表项目，使用 OLED 显示、MPU6050 六轴传感器、按键交互，实现时间显示、菜单系统、设置时间、计步与小游戏（小恐龙）等功能。代码含详细中文注释，适合作为嵌入式学习与简历项目。

## 功能特性

| 模块 | 说明 |
|------|------|
| 时间显示 | 基于 RTC 实时时钟，OLED 显示年月日时分秒 |
| 菜单系统 | 多级菜单切换，按键上下选择、确认进入 |
| 时间设置 | 支持手动调整时间并写回 RTC |
| 传感器 | MPU6050 六轴姿态数据采集（陀螺仪 + 加速度计）|
| 计步功能 | 基于加速度变化检测步数 |
| 小游戏 | OLED 上的小恐龙跳跃游戏 |
| 硬件驱动 | 自写软件 I2C 驱动 MPU6050，硬件 I2C 驱动 OLED |

## 硬件平台

- 主控：STM32F103（大容量型号）
- 显示：0.96 寸 OLED（SSD1306，I2C 接口）
- 传感器：MPU6050（六轴，I2C 接口）
- 交互：多路按键输入
- 开发环境：Keil MDK 5.x（ARMCC）

## 目录结构

```
├── Hardware/          用户硬件驱动层
│   ├── OLED.c/h       OLED 显示驱动
│   ├── OLED_Data.c/h  OLED 字库与图形数据
│   ├── MPU6050.c/h    MPU6050 传感器驱动
│   ├── MyI2C.c/h      软件模拟 I2C
│   ├── Key.c/h        按键扫描
│   ├── LED.c/h        LED 控制
│   ├── AD.c/h         ADC 采样
│   ├── SetTime.c/h    时间设置界面
│   ├── menu.c/h       菜单系统
│   └── dino.c/h       小恐龙游戏
├── Library/           STM32 标准外设库（StdPeriph Driver）
├── Start/             启动文件与 CMSIS 内核文件
├── System/            系统级工具
│   ├── Delay.c/h      精确延时
│   ├── MyRTC.c/h      RTC 时钟封装
│   └── Timer.c/h      定时器封装
├── User/              应用层
│   ├── main.c         程序入口与主循环
│   ├── stm32f10x_it.c 中断服务函数
│   └── stm32f10x_conf.h 外设库配置
├── Project.uvprojx    Keil 工程文件
└── keilkill.bat       清理编译中间文件脚本
```

## 编译与烧录

1. 用 **Keil MDK 5** 打开 `Project.uvprojx`
2. 确认已安装 `STM32F10x` 器件支持包（Keil.STM32F1xx_DFP）
3. `Project → Build Target`（或 `F7`）编译
4. 连接 ST-Link / J-Link，`Flash → Download`（或 `F8`）烧录

> 若编译后想清理中间文件，可直接运行 `keilkill.bat`。

## 说明

- `Objects/`、`Listings/`、`*.uvguix.*` 等编译产物与个人配置已通过 `.gitignore` 排除，仓库只保留源码与工程配置。
- 换行符统一由 `.gitattributes` 管理，保证 Windows 下用 Keil 打开格式正常。

## License

本项目仅用于学习与交流。
