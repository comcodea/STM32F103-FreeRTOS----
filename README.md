# FreeRTOS 移植项目架构文档

## 项目概述

本项目是基于 STM32F103 的 FreeRTOS 移植工程，主要实现了 FreeRTOS 在 STM32F1 系列芯片上的运行环境配置和基础功能验证。

- **项目名称**：实验0-3的HAL版本
- **实验平台**：普中 F103 精灵低配 开发板
- **实验目的**：学习基于HAL版本的MDK开发

## 2. 目录结构

```
project/
├── FreeRTOS移植/
│   ├── Projects/
│   │   ├── Drivers/
│   │   │   ├── BSP/          # 板级支持包
│   │   │   ├── CMSIS/        # Cortex微控制器软件接口标准
│   │   │   ├── STM32F1xx_HAL_Driver/  # STM32 HAL驱动
│   │   │   └── SYSTEM/       # 系统相关驱动
│   │   ├── Middlewares/
│   │   │   ├── FreeRTOS/     # FreeRTOS实时操作系统
│   │   │   ├── MALLOC/       # 动态内存管理
│   │   │   └── USMART/       # 用户交互模块
│   │   ├── Output/           # 输出文件
│   │   ├── Projects/         # 项目文件
│   │   └── Users/           # 用户代码
│   ├── readme.md
└── arch.md
```

## 3. 核心模块

### 3.1 FreeRTOS

- **功能**：实时任务调度、事件管理、队列通信等。
- **关键文件**：
  - `tasks.c` - 任务管理
  - `queue.c` - 队列实现
  - `event_groups.c` - 事件组实现

### 3.2 STM32 HAL驱动

- **功能**：提供硬件抽象层接口，简化外设操作。

### 3.3 动态内存管理

- **功能**：提供动态内存分配与释放功能。

## 4. 依赖关系

- FreeRTOS 依赖于 STM32 HAL 驱动和 CMSIS 标准库。
- 用户代码通过 FreeRTOS API 和 HAL 驱动与硬件交互。
