# DX-SMART LoRa Module Troubleshooting Guide / 模块无法使用排查指南

If your LoRa development board or module is not working or failing to program, please follow the step-by-step checklist below to diagnose and resolve the issue.

如果您在使用或烧录 LoRa 模块时遇到问题，请按照以下步骤逐步排查。

---

## Step 1: Identify Your Development Board Version / 确认您的开发板版本

Before configuration, you must check which hardware version of the development board you are using (**PJ23** or **PJ26**). Different versions require different RTS/DTR pin controls.

在开始配置前，请先确认您手中的开发板硬件版本（**PJ23** 或 **PJ26**），不同版本对应的 RTS/DTR 控制模式不同。

* **How to identify:** Refer to the silk-screen marking on the board or check the structural differences in the image below.
* **如何识别：** 请观察板子上的丝印型号，或对比下方图片的硬件外观。

<img width="1338" height="590" alt="对比图" src="https://github.com/user-attachments/assets/0ce6cac6-5f85-445a-a9eb-83e50b15c8b8" />

---

## Step 2: Configure the MCUISP Programming Tool / 配置 MCUISP 烧录工具

Open the **MCUISP** software and ensure the following 3 settings are correctly configured:
打开 **MCUISP** 软件，确保以下 3 处设置完全正确：

1. **Port & Baudrate (串口与波特率):** Select the correct COM port and set the baudrate to **`460800`**.
2. **Firmware Path (固件路径):** Load the correct `.hex` file.
3. **RTS/DTR Control (RTS/DTR 控制):** Click the dropdown menu at the bottom left and select the mode based on your board version:
   * **For PJ23:** Select `Reset@DTR Low(<-3V), ISP@RTS High`
   * **For PJ26:** Select `Reset@DTR High(>+3V), ISP@RTS Low`
    
<img width="850" height="946" alt="串口设置图" src="https://github.com/user-attachments/assets/0166b331-9474-4310-86a0-787dc7b100d5" />

---

## Step 3: Read Chip Information / 读取芯片信息

1. Click the **"Read ChipInfo(R)"** button in MCUISP.
2. **Crucial Action:** Immediately press the **RST (Reset) button** on the development board to trigger the bootloader.

1. 点击 MCUISP 的 **"Read ChipInfo(R)"** 按钮。
2. **关键操作：** 紧接着按下开发板上的 **RST 复位键**，以触发芯片进入下载模式。
   
<img width="4094" height="3072" alt="c57c3fe606a4b4ac1948e7693c1ae9f9" src="https://github.com/user-attachments/assets/46920da7-ad96-4fe1-98a9-d0edb49187d4" />
<img width="840" height="874" alt="烧录成功" src="https://github.com/user-attachments/assets/ba1a258d-a0b1-46a4-a606-bf8442eb0006" />


* **If it succeeds:** The chip info will log in the window, meaning the hardware connection and programming settings are correct. (如果您能看到芯片信息输出，说明硬件连接与烧录设置正常)。
* **If it fails (Error prompt appears):** Please proceed to **Step 4** to perform an isolated module test. (如果出现错误提示，请继续执行 **Step 4** 隔离测试模块)。

---

## Step 4: Isolated Module Serial Test / 模块独立串口测试（验证程序是否存在）

If MCUISP cannot read the chip, we need to verify if the module already contains firmware and can boot normally.

如果烧录工具无法读取芯片，我们需要通过普通串口软件测试模块内是否有现成程序、以及它是否能正常工作。

1. Close MCUISP, and open your standard **UART Assistant (Serial Tool)**.
2. Configure the serial options: **Baudrate: `9600`**, Data bits: `8`, Stop bits: `1`, Parity: `NONE`.
3. Press the **RST button** on the board and observe the data log receiver window.

1. 关闭 MCUISP，打开普通的 **串口调试助手**。
2. 配置串口参数：**波特率 `9600`**，数据位 `8`，停止位 `1`，校验位 `NONE`。
3. 按下板子上的 **RST 复位键**，观察数据接收窗口。
<img width="587" height="654" alt="测试图" src="https://github.com/user-attachments/assets/a430c2c0-0a84-4136-a2d9-62337798667f" />


### How to Analyze the Result / 结果分析：

* **Scenario A (Firmware Exists / 有程序本地运行):** If you see initial boot messages like `---> Power On`, firmware version (e.g., `---> V1.2.35`), or module model (`---> DX SX1262...`), **the module has a valid program and is booting correctly.** Please re-check your MCUISP programming settings or USB cable.
  *如果按下 RST 键后，窗口打印出 `---> Power On`、版本号或模块型号等响应信息，说明**模块内部已有完整程序且能正常启动**。请重新检查烧录软件设置或 USB 数据线。*

* **Scenario B (Blank Chip / 无程序无响应):** If the window remains completely blank (no response at all) after pressing the RST button multiple times, **the chip might be empty or in a deep halt.** Please return to **Step 2** and double-check if your RTS/DTR hardware flow control matches your board model (PJ23/PJ26).
  *如果多次按下 RST 键后，窗口完全没有任何数据返回，说明**芯片内可能没有程序或处于死机状态**。请返回 **Step 2**，重点检查 RTS/DTR 硬件流控制开关是否与您的板子型号（PJ23/PJ26）严格匹配。*

---

## 📞 Still Need Help? Contact Us / 联系我们

If the module still does not work after following all the troubleshooting steps above, please feel free to contact our technical support team. We will help you resolve the issue as soon as possible.

如果您在尝试了以上所有排查步骤后模块依然无法使用，请随时联系我们的技术支持团队，我们将竭诚为您解决问题。

* **📧 Email:** [Your Support Email / 你们公司的客服或你的工作邮箱]
* **🌐 Website:** [Your Company Website / 深圳大夏龙雀科技官网链接]
* **🏢 Company:** Shenzhen DX-SMART Technology Co., Ltd. (深圳大夏龙雀科技有限公司)
