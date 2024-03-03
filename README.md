
本次DIY要用到最近挺火的磁流体，制作一个酷炫音箱，效果非常的nice~
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/47bca5e4-eb74-4a75-b191-7d6ad27738fa)


磁流体是一种遇到磁场形态会发生“神奇”变化的流体，如果将美妙的音乐信号转化为电流信号来控制电磁铁从而作用于磁流体会是怎样的呢？答案是：very cool！~

那还等什莫？干就完事！

具体思路：将蓝牙功放板的一路音频信号输出给esp32的ADC引脚，将音频的模拟信号转化为数字信号，再输出pwm给电机模块来控制电磁铁，从而产生一个“音乐磁场”，让磁流体在这个磁场里“跳舞”~

一.材料准备：
瓶装磁流体，esp32开发板，12v60kg吸力电磁铁，蓝牙功放板，运算放大模块，L298N电机模块，面包板电源，0.91寸OLED显示屏，4位数码管（TM163X驱动），12V电源适配器，喇叭，10*10洞洞板，亚克力切割外壳，亚克力专用胶水，杜邦线。（还有开关，电位器）

工具要用到电烙铁，胶布，热熔胶枪。
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/ff1c6e92-195d-4dd9-820c-4762a31a6b91)


注意是低密度磁流体，有点贵~
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/de0b4653-16b2-4c10-9885-6403759fbfe3)


电磁铁吸力太大或太小都会导致效果不好，两根线不分正负接L298N控制输出接口
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/864bb8dc-c822-477e-8c10-2038dafa230a)


考虑到音质不用esp32自带的蓝牙，5v供电，两个喇叭接口要留一个输出音频信号给开发板ADC引脚（音频信号电压值太小的话开发板检测不到，可以用个信号放大模块）

![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/00192cb7-454e-46f7-95ad-72d9f2db35ab)

L298N用来控制电磁铁，12v供电，控制输入引脚接开发板，输出接电磁铁~

![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/c5163dfa-65a6-48a0-819e-50e31121ed70)

用来给各模块和开发板供电，电源输入接电源适配器~

![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/d18f8abc-0b46-4beb-ae24-7aa037a7a7f7)

显示屏嘿嘿，用来显示音频波形啥的，增加炫酷值~
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/877233c3-874e-4ba4-8e63-06167dc20d2a)


数码管可以用来显示时间，功能+1 ~
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/e29d4fdd-fb16-491c-bf57-87b16b1f3066)


开发板esp-wroom32,便宜又好用，(ST fu*k 油~)
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/c9842c68-c835-4856-a51b-0ecc566b9fba)


喇叭选了个便宜的，有点后悔，应该买个好点的~

二.电路连接:
示意图，看个大概
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/38f59e8d-94c5-4ac3-b63c-ea8838a31d48)


更新：可抄作业的连线图：
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/9ddcef4c-fdcb-4a72-8f38-5e8fa6970e4f)


实物图（飞线飞啊飞~）：
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/cedcb52c-227e-4b7d-8827-74cd6b74d56f)


三：外壳设计
用不起3d打印~，亚克力YYDS~(最后发现亚克力外壳+胶水的效果比打印件还要好看一点~）
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/854c94d7-6ba5-4ed8-a5fe-85bb2093e21c)

以下是亚克力切割图
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/44b2eb7e-6365-4942-999c-8cbc9d0e48ee)


四：组装：

下面黑色盒子装电路板
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/7698de7b-360d-47d3-9eea-59e065d2245c)


乐高和热熔胶万能的~（磁流体两边是灯条）
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/0e542fae-7fa4-4a94-8b1b-108025454c2c)

![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/7f5aacdb-82aa-4cf1-93f3-f91e0732684d)

背面
五：代码：
10.5更新：这里讲一下Arduino，Arduino是一个开源的电子设计平台，聚集了众多电子Diy爱好者，网上有大量入坑教程，对新手及其友好~（当然此次Diy可以直接下个arduino，搭好esp32的开发环境，烧录我的代码就行~）

代码中调用了两个库，需要在arduino软件打开库管理器安装这两个库才能让代码编译通过：
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/7dc9f9e8-4067-49c3-b334-4aa7f5113a5a)



代码没啥好讲的，数码管，OLED屏幕，wifi都有方便的库可以调用。下面四行代码就是将音频模拟信号转换为PWM信号的过程，改变代码可以可实现不同磁流体效果。
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/de1d40a5-0d41-4dcd-bfa4-795adf7d2549)


！完整的代码放在文章最后~

六：才艺表演：（声音有点小，大家请调大音量欣赏~）
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/d2de134c-728d-4a8d-b452-af3590981596)
![image](https://github.com/MIN-QS/-ESP32---/assets/162037140/b73e26c2-a0da-4ffc-8240-80b81b0d7eeb)


