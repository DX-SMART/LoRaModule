
# LoRa Modules

## LORA-001 — Firmware Upgrade

**Q: Can I upgrade the LoRa module firmware by myself?**

**A:** No. The LoRa module does not support user-side firmware upgrades.

If a firmware upgrade is required, please contact us and return the module to our company. Our technical team will perform the firmware upgrade.


---

## LORA-002 — Arduino / ESP32 Compatibility

**Q: Can the LoRa module be used with Arduino or ESP32?**

**A:** Yes. Our LoRa modules can be used with Arduino and ESP32. However, the application code needs to be developed by the customer.

We currently do not provide programming or development support for Arduino or ESP32.

For some non-development modules, such as **LR01, LR22, and LR32**, Arduino examples are available for reference.


---

## LORA-003 — Frequency Band Configuration

**Q: Can the LR20 / LR30 frequency band be changed?**

**A:** Yes. The **LR20 and LR30** support changing the operating frequency band through programming.

The supported frequency ranges are:

| Version | Frequency Range |
|---|---|
| 433 version | 433–470 MHz |
| 900 version | 850–930 MHz |

Please refer to the product documentation for the detailed supported frequency bands.


---

## LORA-004 — Programming Failure

**Q: What should I do if programming fails?**

**A:** If the program cannot be successfully flashed to the device, you can try using an **ST-Link** to reprogram the device firmware.


---

## LORA-005 — Mobile Phone Operation

**Q: Can I operate the LoRa module directly from a mobile phone?**

**A:** No. The LoRa module cannot directly communicate with a mobile phone, so it cannot be directly operated through a phone.

---

## LORA-006 – Original Factory Firmware Location

**Q: Where can I find the original factory firmware (HEX file) to restore the device?**

**A:** You can find the original factory firmware (`DX_TESET.hex`) inside the provided resource package. Unzip the package and navigate to the following path:

`07 Programming code demonstration` -> `LR20&30-900` -> `LR20&30-900` -> `Project` -> `Objects`

Inside the **Objects** folder, locate **`DX_TESET.hex`** and re-flash it onto the MCU (STM32F103C8T6) using an **ST-Link**, **J-Link**, or **Serial ISP tool** to restore the default factory settings.

<img width="696" height="625" alt="image" src="https://github.com/user-attachments/assets/16856f6c-1e94-4ce7-89de-92f833f0a1fd" />


## LORA-007- LR02/LR22/LR32/LR42 Cannot Enter AT Mode or Communicate with Each Other

**Q: What should I do if the LR02/LR22/LR32/LR42 cannot enter AT mode or cannot communicate with each other?**

**A:** Troubleshooting Steps

#### 1. Check whether the computer can recognize the COM port

First, check whether the computer can correctly recognize the module's **COM port** after the module is connected.

If the COM port is not detected, check:

* Whether the USB-to-Serial driver is installed correctly.
* Whether the USB cable is working properly.
* Whether the connection between the module and the USB-to-Serial adapter is correct.
* Whether the corresponding COM port appears in **Device Manager**.

---

#### 2. Check the serial port parameters and line ending settings

Check whether the serial port parameters are configured correctly, especially:

* **Baud Rate**
* **Parity**
* Other serial communication parameters

Also make sure that **Auto Append Bytes** is enabled.

Enter:

```text
0D 0A
```

**Note:** `0D 0A` contains the number **0**, not the letter **O**.
<img width="667" height="575" alt="1425ff128a3ccd2cc637db09e6523c75" src="https://github.com/user-attachments/assets/132447b7-4e4a-4e2e-9b35-9c96a5ffe33b" />


---

#### 3. Send `2B 2B 2B` in HEX mode to check whether the module can enter AT mode

Switch the serial debugging software to **HEX mode**.

Enter:

```text
2B 2B 2B
```

Then send the command.

Check whether the module can successfully enter **AT mode**.
<img width="667" height="575" alt="b5052c7a0e0cf123e7e6a8b284f3e4f9" src="https://github.com/user-attachments/assets/e2af5c32-b192-4796-9837-b92ddce8d4a1" />


### If the module can enter AT mode

Switch the serial debugging software back to **ASCII mode**.

Then send:

```text
AT+DEFAULT
```

This will **restore the module to factory default settings**.

After restoring the factory settings, perform the communication test between the modules again.

### If the modules still cannot communicate

Recheck the communication parameters of both modules and make sure they are configured correctly before testing again.




