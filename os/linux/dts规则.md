
设备树文件，第一行：版本描述
在版本描述之后，设备树以一个斜杠“/”开始，表示树的根。
然后是大括号。

设备树与文件系统做比较（事实上内核真的实现了这个文件系统/proc/device-tree）：
	每个大括号表示一个目录，目录名是大括号前的字符串，冒号之前的是标签（标签只出现在DTS文件中，而不出现在DTB文件）。
		例如:	标签：目录名
				{
					文件名 = 文件内容；
				}







uart0:serial@44e0900{
	compatible=
	ti,hwmods=
	


}

寄存器地址：44e0900
compatible：定义设备的programming model 
			兼容性
			用于匹配设备节点和设备驱动
			要与驱动代码中的.compatible匹配一致。
address：
	address-cells：描述子节点reg属性值地址表中首地址cell数量。
	size-cells：描述子节点reg属性值的地址表中地址长度cell数量。
clock-frequency:频率
reg；寄存器(起始)地址和寄存器长度
	描述地址表，I/O地址。
ranges：有些设备是有片选的，所以需要描述片选和片选的偏移量，
	在地址说明的时候，还要说明地址映射范围。
interrupt:中断号
interrupt-parent：标识此设备节点属于哪个中断控制器，不设置时，依赖父节点的。
interrupts：中断标识符列表，表示每一个中断输出信号，引用中断号及中断触发类型。
interrupt-cells：中断控制器节点属性，标识这个控制器需要几个单位做中断描述符。
interrupt-controller：一个空属性，用来声明这个node接收中断信号。
status：状态值，初始为disabled ，则表示禁用
gpio：
gpio-controller：描述的是一个gpio控制器

chosen节点：并不代表一个真正的设备，而是用来在Firmware与操作系统间传递数据，如启动参数。
通常chosen节点在dts中被置空。


节点命名应该反映设备的类型， 而不是特点型号。
	例如：3com的以太网卡，通常节点名就叫ethernet而不叫3com509。



属性设置的套路：
	第一种：抄袭类似的dts，比如项目平台是4412，那么就可以抄exynos4412-tiny4412.dts、
		exynos4412-smdk4412.dts这类相近的dts
	第二种：查询内核中的文档，比如Documentation/devicetree/binding/i2c/i2c-imx.txt就
		描述了imx平台的i2c属性设置方法；Documentation/devicetree/binding/fb就描述了
		lcd、lvds这类属性设置方法。



