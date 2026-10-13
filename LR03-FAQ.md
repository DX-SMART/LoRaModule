### DX-LR03-900T30D RF Output Power

**Q: Why does the DX-LR03-900T30D return error code 101 when executing `AT+POWE20`?**

**A:** The parameter setting range for AT+POWE is 0 to 18; values ​​outside this range will result in an error. Although the module's theoretical maximum transmit power is 28 dBm, the actual measured maximum is approximately 26.82 dBm due to factors such as RF link losses. The module is set to maximum transmit power by default; please refer to Section 5.3.3 of the application manual for the specific mapping between parameters and actual transmit power.
