# Graduation-project

毕业设计项目的硬件资料。

## 项目列表

| 目录 | 说明 | 状态 |
|---|---|---|
| [`hardware/stm32-environment-monitor`](hardware/stm32-environment-monitor) | **基于 STM32 的多功能环境智能监控系统**：温湿度、光照、RTC、OLED、按键、LED、蜂鸣器、12V 灯带控制，12V 输入板载降压 | V1.2，已提交嘉立创打样 |
| [`hardware/parking-bluepill`](hardware/parking-bluepill) | 基于 Blue Pill 的车位相关电路（KiCad 工程） | 草稿 |

## 环境监控板（V1.2）简介

- 主控：立创·地阔星 STM32F103C8T6 开发板，插在 2×20 排母上。
- 传感与显示：GXHT30C 温湿度、SD3077 实时时钟（CR1220 备份电池）、0.96" OLED（4P 母座）、光敏电阻。
- 输出：有源蜂鸣器、红/绿/黄 LED、12V LED 灯带（AO3400A 开关）。
- 输入：4 个按键（PA0~PA3）。
- 供电：12V DC 座 → 保险丝 → XL1509 降压到 5V；3.3V 由开发板 LDO 提供。
- 下载程序：开发板自带 SWD 口，接 DAP-Link；Type-C 只供电。

![接线图](hardware/stm32-environment-monitor/docs/接线图.png)

更多内容（引脚表、BOM、Gerber、装配注意事项）见
[环境监控板 README](hardware/stm32-environment-monitor/README.md)，
原理图见 [`docs/原理图.png`](hardware/stm32-environment-monitor/docs/原理图.png)。

## 工具

- 环境监控板：嘉立创 EDA 专业版（`.epro`）
- 车位电路：KiCad
