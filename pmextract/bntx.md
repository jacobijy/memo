# BNTX图片解析
案例 pm0003_00_00_00.bntx pm0003_00_00_00_big.bntx
# 解析方法
首先还是用二进制打开文件，观察数据构成

前4个字节转化为字符串为BNTX，为通用的magic header
