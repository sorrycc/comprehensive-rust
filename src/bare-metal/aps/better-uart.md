---
translated_at: '2024-03-26T11:43:13.033Z'
---

# 更好的 UART 驱动程序

PL011 实际上还有 [更多的寄存器][1]，为了构造指针以访问这些寄存器而添加偏移量，这样做容易出错，可读性也差。另外，其中一些寄存器是位字段，如果能以结构化的方式访问它们将会更好。

| 偏移量 | 寄存器名称 | 宽度 |
| ------ | ----------- | ----- |
| 0x00   | DR          | 12    |
| 0x04   | RSR         | 4     |
| 0x18   | FR          | 9     |
| 0x20   | ILPR        | 8     |
| 0x24   | IBRD        | 16    |
| 0x28   | FBRD        | 6     |
| 0x2c   | LCR_H       | 8     |
| 0x30   | CR          | 16    |
| 0x34   | IFLS        | 6     |
| 0x38   | IMSC        | 11    |
| 0x3c   | RIS         | 11    |
| 0x40   | MIS         | 11    |
| 0x44   | ICR         | 11    |
| 0x48   | DMACR       | 3     |

<details>

- 还有一些身份寄存器被省略了，为了简洁起见。

</details>

[1]: https://developer.arm.com/documentation/ddi0183/g/programmers-model/summary-of-registers
