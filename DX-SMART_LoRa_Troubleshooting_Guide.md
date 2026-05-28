# DX-SMART LoRa 模块无法使用排查指南

如果您在使用或烧录 LoRa 模块时遇到问题，请按照以下步骤逐步排查。

---

## 步骤 1：确认开发板版本

请先确认您的开发板型号：

* **PJ23**
* **PJ26**

不同版本对应不同 RTS/DTR 控制方式。
<img width="1266" height="558" alt="WPS圖片(1)" src="https://github.com/user-attachments/assets/355335d5-9803-4572-9973-68eb967d96ec" />


---

## 步骤 2：配置 MCUISP

打开 **MCUISP** 软件，确认以下设置：

1. 点击 `EnumPort` 自动识别串口
2. 选择正确 COM 口
3. 波特率设置为 `460800`
4. 加载正确 `.hex` 固件文件
5. RTS/DTR 设置：

### PJ23：

```text id="2jx8gq"
Reset@DTR Low(<-3V), ISP@RTS High
```

### PJ26：

```text id="xg6s2k"
Reset@DTR High(>+3V), ISP@RTS Low
```
<img width="841" height="962" alt="wechat_2026-05-28_110105_842" src="https://github.com/user-attachments/assets/e12a1f38-ef8b-4fcd-a69b-1bb2fdc51284" />

---

## 步骤 3：读取芯片信息

1. 点击：

```text id="4t8lmn"
Read ChipInfo(R)
```

2. 立即按下开发板 `RST` 按键。

### 结果：

* 如果成功读取芯片信息 → 设置正常
* 如果失败 → 继续步骤 4
<img width="864" height="648" alt="image" src="https://github.com/user-attachments/assets/563c3fa0-863e-4e11-adec-da816c91604d" />
<img width="667" height="737" alt="image" src="https://github.com/user-attachments/assets/7f9cd1de-5336-4645-aa5b-fd5b58381637" />


---

## 步骤 4：串口测试

使用串口调试助手测试模块是否正常运行。

### 串口参数：

```text id="3jps7y"
波特率：9600
数据位：8
停止位：1
校验位：NONE
```

按下 `RST` 键观察输出。

### 情况 A：有输出

例如：

```text id="0yr2pn"
---> Power On
---> V1.2.35
---> DX SX1262...
```

说明模块程序正常，请检查：

* MCUISP 配置
* RTS/DTR 设置
* USB 数据线

<img width="554" height="617" alt="image" src="https://github.com/user-attachments/assets/68bae577-4a2e-47dd-93d2-46d51a341ec1" />

---

### 情况 B：无输出

如果完全无任何返回：

* 芯片可能无程序
* RTS/DTR 设置错误
* 板型选择错误

请重新检查 PJ23 / PJ26 设置。

---

# 📞 联系我们

如果问题仍无法解决，请提供以下信息：

1. LoRa 模块型号
2. 开发板型号（PJ23 / PJ26）
3. 问题现象描述
4. 电脑系统（Windows/macOS）
5. 高清报错截图，操作视频，串口输出截图（这将帮助我们更快速定位问题。）

---

📧 Email: manager@szdx-smart.com
💬 WhatsApp: +86 15798463070
🏢 深圳大夏龙雀科技有限公司
Shenzhen DX-SMART Technology Co., Ltd.
