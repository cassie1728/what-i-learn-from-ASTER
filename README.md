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
    2. 使用弯曲文本检测器做预训练模型。
    3. 使用基于像素点检测的模型，做像素点的二分类（前景or背景），再找前景区域的外接多边形，根据外界多边形的边界矫正。
    
#### 补充

