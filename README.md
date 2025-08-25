# FreeRTOS 移植项目架构文档

## 项目概述

本项目是基于 STM32F103 的 FreeRTOS 移植工程，主要实现了 FreeRTOS 在 STM32F1 系列芯片上的运行环境配置和基础功能验证。

## 模块划分

1. **Drivers**
   - `CMSIS/`: Cortex-M 核心支持库
   - `STM32F1xx_HAL_Driver/`: STM32 HAL 库驱动
   - `SYSTEM/`: 系统级驱动（如时钟、延时、串口等）

2. **Middlewares**
   - `FreeRTOS/`: FreeRTOS 实时操作系统核心
   - `MALLOC/`: 动态内存管理模块
   - `USMART/`: 串口调试工具

3. **Users**
   - `main.c`: 主程序入口，包含任务初始化和主循环
   - `FreeRTOSConfig.h`: FreeRTOS 配置头文件
   - `stm32f1xx_it.c/h`: 中断服务函数

## 关键配置

1. **FreeRTOS 配置**
   - 使用抢占式调度器 (`configUSE_PREEMPTION = 1`)
   - 系统时钟节拍频率为 1000Hz (`configTICK_RATE_HZ = 1000`)
   - 最大优先级数为 32 (`configMAX_PRIORITIES = 32`)
   - 动态内存分配大小为 10KB (`configTOTAL_HEAP_SIZE = 10 * 1024`)

2. **中断配置**
   - 最低中断优先级为 15 (`configLIBRARY_LOWEST_INTERRUPT_PRIORITY = 15`)
   - FreeRTOS 可管理的最高中断优先级为 5 (`configLIBRARY_MAX_SYSCALL_INTERRUPT_PRIORITY = 5`)

## 功能描述

1. **主程序**
   - 初始化 HAL 库和系统时钟
   - 配置 LED 控制 GPIO
   - 主循环中实现 LED 闪烁功能

2. **FreeRTOS 功能**
   - 支持任务创建、删除、挂起和恢复
   - 支持软件定时器和队列
   - 提供任务运行时间统计功能
