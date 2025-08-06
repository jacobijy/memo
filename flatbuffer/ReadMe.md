# 二进制文件读写
## 例子 personal_array.bin
### 初始位置
初始bb_pos = 0， 然后读取位于pos的4个字节uint32
前4字节为 0C 00 00 00<br/>
因为小端读写， 00 00 00 0C， 初始bb_pos = 12<br/>
### vector-length读取
从初始位置开始读取4字节的int的offset<br/>
offset = __offset(bb_pos, 4)  结果为<br/>
```
vtable = bb_pos - readint32(bb_pos) // vtable = 12 - 6 (06 00 00 00) = 6
read16(vtable + 4) // read16(10) --- 04 00 结果为4
```
```
length = __vector_len(bb_pos + offset) // __vector_len(12 + 4)
read32(16 + read32(16))     // read32(16 + 4) = read32(20) --90 05 00 00
```
结果1424
### vector 数据片段读取
获取初始位置
首先获取 offset = __offset(bb_pos, 4) 结果同上为4
```
    __vector(this.bb_pos + offset) // __vector(16)
    16 + read32(16) + 4 // 16 + 4 + 4 = 24
```
```
    __indirect(vector) // __indirect(24)
    24 + read32(24) // 
```