# DX-SMART LoRa Module Troubleshooting Guide 

If your LoRa development board or module is not working or failing to program, please follow the step-by-step checklist below to diagnose and resolve the issue.


---

## Step 1: Identify Your Development Board Version 

Before configuration, you must check which hardware version of the development board you are using (**PJ23** or **PJ26**). Different versions require different RTS/DTR pin controls.

* **How to identify:** Refer to the silk-screen marking on the board or check the structural differences in the image below.

<img width="1338" height="590" alt="对比图" src="https://github.com/user-attachments/assets/0ce6cac6-5f85-445a-a9eb-83e50b15c8b8" />

---

## Step 2: Configure the MCUISP Programming Tool 

Open the **MCUISP** software and ensure the following 3 settings are correctly configured:

1. **Port & Baudrate:** Select the correct COM port and set the baudrate to **`460800`**.
2. **Firmware Path:** Load the correct `.hex` file.
3. **RTS/DTR Control):** Click the dropdown menu at the bottom left and select the mode based on your board version:
   * **For PJ23:** Select `Reset@DTR Low(<-3V), ISP@RTS High`
   * **For PJ26:** Select `Reset@DTR High(>+3V), ISP@RTS Low`
    
<img width="850" height="946" alt="串口设置图" src="https://github.com/user-attachments/assets/0166b331-9474-4310-86a0-787dc7b100d5" />

---

## Step 3: Read Chip Information 

1. Click the **"Read ChipInfo(R)"** button in MCUISP.
2. **Crucial Action:** Immediately press the **RST (Reset) button** on the development board to trigger the bootloader. 
<img width="4094" height="3072" alt="c57c3fe606a4b4ac1948e7693c1ae9f9" src="https://github.com/user-attachments/assets/46920da7-ad96-4fe1-98a9-d0edb49187d4" />
<img width="840" height="874" alt="烧录成功" src="https://github.com/user-attachments/assets/ba1a258d-a0b1-46a4-a606-bf8442eb0006" />


* **If it succeeds:** The chip info will log in the window, meaning the hardware connection and programming settings are correct. 
* **If it fails (Error prompt appears):** Please proceed to **Step 4** to perform an isolated module test. 

---

## Step 4: Isolated Module Serial Test

If MCUISP cannot read the chip, we need to verify if the module already contains firmware and can boot normally.



1. Close MCUISP, and open your standard **UART Assistant (Serial Tool)**.
2. Configure the serial options: **Baudrate: `9600`**, Data bits: `8`, Stop bits: `1`, Parity: `NONE`.
3. Press the **RST button** on the board and observe the data log receiver window.
<img width="587" height="654" alt="测试图" src="https://github.com/user-attachments/assets/a430c2c0-0a84-4136-a2d9-62337798667f" />


### How to Analyze the Result 

* **Scenario A (Firmware Exists ):** If you see initial boot messages like `---> Power On`, firmware version (e.g., `---> V1.2.35`), or module model (`---> DX SX1262...`),
* **the module has a valid program and is booting correctly.** Please re-check your MCUISP programming settings or USB cable.
 
* **Scenario B (Blank Chip ):** If the window remains completely blank (no response at all) after pressing the RST button multiple times,
* **the chip might be empty or in a deep halt.** Please return to **Step 2** and double-check if your RTS/DTR hardware flow control matches your board model (PJ23/PJ26).


---

## 📞 Still Need Help? Contact Us 

If the module still does not work after following all the troubleshooting steps above, please feel free to contact our technical support team. We will help you resolve the issue as soon as possible.


* **📧 Email:** Email: manager@szdx-smart.com
* **💬 WhatsApp:**  +86 15798463070
