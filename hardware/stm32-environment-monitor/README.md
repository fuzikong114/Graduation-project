# STM32 环境监控系统硬件 V1.0（模块版）

基于 STM32F103C8T6 Blue Pill 核心板。传感器、显示屏和 RTC 都用 4P 排针外接模块。

## 文件

| 文件 | 说明 |
| --- | --- |
| `STM32-Environment-Monitor-V1.0.epro` | 嘉立创 EDA 专业版工程（原理图 + PCB1），可直接导入编辑 |
| `fabrication/Gerber_STM32_Env_Monitor_V1.0.zip` | 打板用 Gerber + 钻孔文件，可直接上传嘉立创下单 |
| `fabrication/BOM_STM32_Env_Monitor_V1.0.csv` | 物料清单 |
| `fabrication/PickAndPlace_STM32_Env_Monitor_V1.0.csv` | 贴片坐标文件 |
| `archive/STM32-Environment-Monitor-SMD-DRAFT.epro` | 未完成的贴片传感器 / OLED 裸屏方案草稿，**不要用于打板** |

## 板子参数

- 双层板，157.99 × 105.54 mm，顶层和底层都铺了 GND 铜
- 12V 输入、灯带回路走线 40 mil，信号线 10 mil
- 嘉立创 EDA 设计规则检查：原理图 0 错误；PCB 141 项检查 0 问题，没有未布线的网络

## 接口与引脚

| 功能 | Blue Pill 引脚 | 说明 |
| --- | --- | --- |
| KEY1–KEY4 | PA0–PA3 | 按下接 GND，固件里开内部上拉 |
| LED 红 / 绿 / 黄 | PB0 / PB1 / PB10 | 红、黄低电平亮，绿高电平亮 |
| I2C1 SCL / SDA | PB6 / PB7 | 板上 4.7k 上拉到 3V3 |
| 灯带 MOS 管 (AO3400) | PA11 | 高电平点亮；PA11 同时是 USB D-，调试用 SWD |
| 有源蜂鸣器 (S8050) | PA8 | 高电平响 |
| SWD | PA13 / PA14 | J11 接 ST-LINK，J12 接 Blue Pill 的 SWD 排针 |

模块接口 J3–J6 的引脚顺序是 `1:3V3 2:GND 3:SCL 4:SDA`，I2C 地址：SHT30 0x44、BH1750 0x23、SSD1306 0x3C、DS3231 0x68。

## 装配前请核对

1. **模块引脚顺序。** 很多 0.96 寸 OLED 模块是 `GND VCC SCL SDA`，和本板的 J5（`3V3 GND …`）前两脚是反的；DS3231 模块（如 ZS-042）引脚也不是这个 4P 顺序。插模块前先对照丝印，不一致就用杜邦线交叉接。
2. **模块自带上拉。** 板上已经有 4.7k 上拉；模块自带的上拉过多时，可以拆掉部分。
3. **LM2596 输出。** 先把 LM2596 模块调到 5.0V，再接 J10 和 Blue Pill。
4. **USB 和外部 5V 不能同时供电。**
5. **保险丝。** FH1 装 T2A 5×20 保险丝。
