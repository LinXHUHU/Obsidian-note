
# CRC 计算模式
1. **E2E_P01_DATAID_BOTH：** 在这种模式下，CRC 计算涉及两个字节的数据 ID。首先计算低字节（LSB）的 CRC，然后计算高字节（MSB）的 CRC，最终结果是两个 CRC 的组合。
    
2. **E2E_P01_DATAID_LOW：** 只计算低字节（LSB）的 CRC，高字节（MSB）被忽略。
    
3. **E2E_P01_DATAID_ALT：** 在这种模式下，根据计数器的奇偶性选择计算低字节（LSB）或高字节（MSB）的 CRC。如果计数器是偶数，则计算低字节的 CRC；如果是奇数，则计算高字节的 CRC。
    
4. **E2E_P01_DATAID_NIBBLE：** 计算低字节（LSB）的 CRC，然后再计算一个字节的 CRC，这个字节的值是 `0x00`。


# 调用架构很简单

![[Drawing 2023-11-21 10.07.24.excalidraw]]

主要是底层profile计算实现，crc校验

顶层的通用调用架构