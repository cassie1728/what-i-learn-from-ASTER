# Papers about Text Recognition No.1

## ASTER (带有矫正网络的识别模型)
My understanding about the paper ASTER:An Attentional Scene Text Recognition with Flexible Rectification

### 关于ASTER这篇论文，主要内容在ppt中均有提到，讲解在备注中。

#### pipeline

![](https://github.com/cassie1728/what-i-learn-from-ASTER/raw/master/aster1.jpg)

#### 总结：

ASTER 的优点在于加入了矫正网络，rectification network 基于STN网络，使用了TPS变换来拟合透视、弯曲等非刚性变换。<br>

识别网络使用了带attention机制的seq2seq模型，采用双向解码有效提高精度。<br>

#### 思考

![](https://github.com/cassie1728/what-i-learn-from-ASTER/raw/master/aster2.jpg)

ASTER的最终识别效果，很大程度上由矫正效果决定，而矫正网络的关键是控制点坐标的学习（在STN中是TPS变换参数的学习），通过一个简单的CNN网络实现。<br>

所以这个CNN网络很关键。在ASTER的原论文中，CNN：6个卷积层+5个max_pooling夹在其中+2个全连接层，矫正效果由CNN训练情况直接决定，在训练时，最后一个全连接层不使用随机初始化，而是初始化为N(0,a)。<br>

    设想：<br>
    1. 可以加深CNN层数，增大模型复杂程度。
    2. 迁移学习，使用弯曲文本检测网络做预训练模型，简化训练（提供训练初期参数）。
    3. 使用基于像素点检测的模型，做像素点的二分类（前景or背景），再找前景区域的外接多边形，根据外界多边形的边界矫正。
    
#### 补充

　　在我读论文时有点混淆ASTER和STN的Localization Network部分，这两篇的实现并不太一样。<br>
![](https://github.com/cassie1728/what-i-learn-from-ASTER/raw/master/stn.jpg)<br>
　　在STN中，CNN网络直接回归出，变换矩阵T的各个参数![](http://chart.googleapis.com/chart?cht=tx&chl=$\theta$)。参数矩阵（仿射变换）可以实现图片的裁剪、旋转、缩放、倾斜、平移。<br><br>
　　补充解释cropping的实现：如果乘的参数矩阵左边的2![](http://chart.googleapis.com/chart?cht=tx&chl=$\times$)2子矩阵（控制大小的参数）行列式小于1，则相当于对图片做了压缩，那么通过grid对应到原图中的四边形的面积就比原图小（在小于原图区域内取点）。
   <br><br>
　　而在ASTER中，CNN生成控制点K个（2K个坐标参数），然后通过控制点之间的对应求TPS的变换矩阵T。
   <br><br>
　　所以，两个CNN生成的参数是不一样的，但是我觉得ASTER首先生成控制点的方法，有点麻烦，暂时不知道对识别率提高有没有作用。不过，这样确实更方便可视化……
   
