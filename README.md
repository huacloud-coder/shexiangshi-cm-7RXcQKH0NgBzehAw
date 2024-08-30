
**LOTO****示波器统计曲线和故障分析pass/fail测试**


虚拟示波器可以应用在工业自动化检测中，除了常规的检测波形和测量值参数以外，由多个行业客户定制和验证的统计曲线和故障分析（pass/fail）功能也为工业自动化检测带来极大的便利。


     （一）故障分析（pass/fail）的基础：统计曲线功能


在信号检测的自动化测量中，大部分时间是关心某个测量值随时间变化的趋势，比如在开机检测后，波形的峰峰值是如何变化的。虚拟示波器的统计曲线功能，可以绘制出你关注的某些测量值的变化趋势曲线，如下图所示，示波器测试的信号最大值随着时间变化，从最低的0\.49V逐渐变高，一直到4\.73V，然后又降低到最低，接着缓缓升高并震荡：


 


 


![](https://img2024.cnblogs.com/blog/2597459/202408/2597459-20240830095810648-1492407604.png)


 


 


通过这样的统计曲线，我们可以看到被监测的测量值的变化过程和趋势，从而为后面的故障分析做基础。


统计曲线功能的入口在“非标功能”中的“统计/故障判断”中，如下图所示：


 


![](https://img2024.cnblogs.com/blog/2597459/202408/2597459-20240830095825379-945787652.png)


 


 


（二）统计曲线功能可以观察哪些测量值：


理论上所有测量值，比如“最大值，最小值，峰峰值，有效值，平均值，频率，周期，占空比，正负脉宽，上升时间，下降时间”等等，都可以进行统计曲线的绘制，监测它们的变化趋势曲线。但是 虚拟示波器软件的标准版并没有开放所有这些测量值的统计曲线功能，根据型号不同和客户定制的情况不同，只开放了部分测量值的统计曲线功能。这些可以在统计曲线的配置页面看到。有些示波器型号支持多台级联的情况下，多台设备多通道的测量值的统计曲线绘制：


 


![](https://img2024.cnblogs.com/blog/2597459/202408/2597459-20240830095836667-1166445283.png)


 


 


勾选上的测量值就可以在统计曲线绘图区看到对应的曲线，以不同的颜色区分。并且绘图区会在上下空白处用对应的颜色显示对应曲线的最大和最小数值，如下图所示：


 


![](https://img2024.cnblogs.com/blog/2597459/202408/2597459-20240830095844268-791271193.png)


 


 


（三）统计曲线的控制和现实


统计曲线只有在点击了“开始统计”按钮以后才会开始对测量值进行统计，这个按钮就会变成“停止统计”，点击了“停止统计”以后，就会停止统计曲线的绘制。


为了方便工业自动化测试，这个开始统计或停止统计按钮也可以不通过鼠标点击实现，可以由键盘快捷键或者示波器的IO口实现。


对应的键盘快捷键是“shift”\+“z”, 对应的IO口是GPIO功能的IO2，也就是DE2扩展口的4脚。需要注意的是，如果需要IO2控制这个统计开始停止按钮，需要勾选对应的选项，如下图所示：


 


![](https://img2024.cnblogs.com/blog/2597459/202408/2597459-20240830095851397-91572081.png)


 


 


 勾选了“IO2”开始后，IO2引脚的GPIO会被自动设置为输入，这个输入信号遵循3\.3V TTL数字信号逻辑，由低电平跳变到高电平时，会被识别为点击了“开始统计”按钮，相反，这个输入信号由高电平跳变为低电平时，会被识别为点击了“停止统计”按钮。


“开始统计”被点击或者触发后，会清零之前的统计曲线波形和相关的数据，如果开启了故障pass/fail测试，也会清零故障信息。


（四）故障分析pass/fail测试


在上面的统计曲线的基础上，我们可以为测量值对应的每条统计曲线设定曲线的上下限，在上下限范围内的统计曲线变化被认为是正常的，也就是pass,一旦超过上下限的范围，则认为有故障发生，也就是fail。


故障分析的设定是在如下位置：


 


![](https://img2024.cnblogs.com/blog/2597459/202408/2597459-20240830095859537-396312774.png)


 


 


pass/fail测试的结果会在统计曲线绘图区的下方通过色块和文字表示出来，如下图所示：


 


![](https://img2024.cnblogs.com/blog/2597459/202408/2597459-20240830095909826-224360551.png)


![](https://img2024.cnblogs.com/blog/2597459/202408/2597459-20240830095921681-2120314530.png)


 


 


具体是哪个或者哪几个测量值产生了fault的故障，我们也可以在下面的信息栏里看到，会显示“通道号：测量值”形式的故障信息。


 


![](https://img2024.cnblogs.com/blog/2597459/202408/2597459-20240830095932548-675981157.png)


 


 


为了方便客户在工业自动化的信号检测中，更方便的自动化处理故障分析，比如使用实体的报警灯，或者喇叭，或者和PLC联动实现某些动作，故障发生后，除了在 示波器的上位机软件上显示外，还可以使用IO口输出。我们可以在下图所示位置，选中IO3警报，就会自动将示波器的GPIO功能的IO3，也就是扩展口DE2的10脚设置为输出，IO3同样也是遵循3\.3V TTL 数字逻辑。


 


![](https://img2024.cnblogs.com/blog/2597459/202408/2597459-20240830095941774-967778178.png)


 


 


默认的情况下，如果是PASS状态，那么IO3输出低电平，如果是fail状态，那么IO3将输出高电平。如果需要的是相反的逻辑，那么可以在故障的设置页面勾选“IO3警报逻辑反向”选项：


 


![](https://img2024.cnblogs.com/blog/2597459/202408/2597459-20240830095952200-768429230.png)


 


 


（五）状态清除


统计曲线的历史数据和波形，以及故障分析的结果等，都可以通过点击按钮“清除”进行清空。清空后波形和数据将清零，如果勾选了IO3警报的话，那么IO3的输出状态也会被清除。除了手动点击这个清除之外，“停止统计”后的点击“开始统计”时，也会对统计和故障信息自动清除，如果勾选了“IO2开始”，那么从停止到开始的IO状态切换，也会对统计和故障信息自动清除。


 


![](https://img2024.cnblogs.com/blog/2597459/202408/2597459-20240830100003853-842026346.png)


 


 


（六）设置记忆/保存和导入


以上的统计曲线的设置和故障分析的设置都是可以记忆和另存为配置文件的，配置文件可以手动导入回来。这样在工业自动化检测时会更加便利。关于这部分内容我们会在其他部分专门描述。


关于统计曲线和故障分析的使用，可以参考以下视频演示：


《 示波器 软件功能 演示 之 测量值统计曲线功能演示 以及 自动化检测应用实例》[https://www.bilibili.com/video/BV1RJ411C73h/](https://github.com)


《示波器\-统计曲线2\-故障联动\-自动化检测 自动化集成 信号监测判断 pass/fail测试》


[https://www.bilibili.com/video/BV1h5411u7zP/?vd\_source\=c0bedc6c664e75d3c19935cbda8abe19](https://github.com)


《示波器 统计曲线 故障检测 PASS/Fail 功能优化3 工业自动化 产线检测 自动化检测》


[https://www.bilibili.com/video/BV1Hx4y1b73n/?vd\_source\=c0bedc6c664e75d3c19935cbda8abe19](https://github.com)


《示波器\_多台级联配置记忆\+统计故障分析配置记忆功能(1\)》


[https://www.bilibili.com/video/BV1QcvXe1EG6/?vd\_source\=c0bedc6c664e75d3c19935cbda8abe19](https://github.com):[豆荚加速器](https://yirou.org)


《示波器\_多台级联配置记忆\+统计故障分析配置记忆功能(2\)》


[https://www.bilibili.com/video/BV1iDvQeWEYk/?vd\_source\=c0bedc6c664e75d3c19935cbda8abe19](https://github.com)


《示波器更新: Pass/Fail测试\_统计曲线功能(3\) GPIO控制 自动化检测 工业检测》


[https://www.bilibili.com/video/BV1pqvQeAEvk/?vd\_source\=c0bedc6c664e75d3c19935cbda8abe19](https://github.com)


 


