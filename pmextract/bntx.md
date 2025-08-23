# BNTX图片解析
案例 pm0003_00_00_00.bntx pm0003_00_00_00_big.bntx
# 头文件分析
首先还是用二进制打开文件，观察数据构成

pos用来标识文件读取地址

头文件包含前32个字节, pos = 0， 格式8sIH2BI2H2I (格式参考python struct的格式定义)

前4个字节转化为字符串为BNTX，为通用的magic header，之后4个字节都为0x00，是为magic header的分割标志 pos = 8

读取后4个字节int32, `00 01 04 00`, 为 262400 代表文件version, 版本pos来到12

读取后2个字节short, `FF FE`, 为文件大小端标识， 0xfffe 为小端，0xfeff则为大端pos来到14

读取后续2个byte, `0C`和`40`, 前一个为字节对齐偏移alignmentShift=12， 后一个为targetAddrSize=64，pos来到16

读取后4个字节int32, `BA 01 00 00`结果为442， 为文件名地址，pos来到20

读取后2个字节short, `00 00`, 结果为0, 定义为flag, pos来到22

继续读取2个字节short， `A0 01`, 结果为416，定义为firstBlkAddr，是第一段文件的地址，pos来到24

读取后4个字节int32， `00 10 01 00`，结果为69632，定义为relocAddr，为下一段文件的地址，pos来到28

读取剩余4个字节int32, `68 10 01 00`, 结果为69736，为文件的大小，pos来到32，头文件解析结束


