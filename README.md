# Papers about Text Recognition No.1

## ASTER (带有矫正网络的识别模型)
My understanding about the paper ASTER:An Attentional Scene Text Recognition with Flexible Rectification

### 关于ASTER这篇论文，主要内容在ppt中均有提到，讲解在备注中。

#### pipeline

![](https://github.com/cassie1728/what-i-learn-from-ASTER/raw/master/aster1.jpg)

总结：ASTER 的优点在于加入了矫正网络，rectification network 基于STN网络，使用了TPS变换来拟合透视、弯曲等非刚性变换。<br>

识别网络使用了带attention机制的seq2seq模型，再用双向解码有效提高精度。<br>

#### 思考

![](https://github.com/cassie1728/what-i-learn-from-ASTER/raw/master/aster2.jpg)

