### HTTP2即未来
https://www.villainhr.com/page/2016/09/17/HTTP2%E5%8D%B3%E6%9C%AA%E6%9D%A5
https://slides.com/leopq1949/deck/fullscreen#/


### 子网划分

具体业务中，不用转化成二进制来计算，以下是我的计算方法：

首先记住子网掩码每组可能出现的数字，分别是掩0位0，掩1位128，掩2位192，掩3位224，掩4位240，掩5位248，掩6位252，掩7位254，掩8位255。

然后用256减去该数字，就得到了该子网的地址数。

比如一个地址10.2.3.5/25，换算成子网掩码就是10.2.3.5 255.255.255.128。

用256减128等于128。可以知道该子网有128个地址。然后该子网网络号就是10.2.3.0，可用地址范围是10.2.3.1到10.2.3.126，广播地址是10.2.3.127


128(2^7=128), 64(2^6=64), 32(2^5=32), 16(2^4=16), 8(2^3=8), 4(2^2=4), 2(2^1=2), 1(2^0=1)



https://www.zhihu.com/question/53456814
