---
layout:     post
title:      "Style Transfer: Part 1"
subtitle:   "固定内容固定风格的 Style Transfer"
date:       2019-08-17
author:     "Yineng Xiong"
header-img: "img/2019-08-17/st1.png"
tags:
    - Deep Learning
    - Style Transfer
---

> 今天不想学习，继续补档

## 固定内容固定风格的风格迁移
固定内容固定风格的风格迁移是最早的风格迁移方法, 把图片当作可以训练的变量, 通过优化图片来降低与内容图片的 `内容差异` 和 与风格图片的 `风格差异`, 经过迭代后生成的图片会有与内容图片一致的内容, 与风格图片一致的风格.

## 内容损失与风格损失
经典的风格迁移都是通过 __VGG__ 来衡量 __Content Loss__ 和 __Style Loss__.

图片经过一个 __VGG16__ 的编码器, 每个 `MaxPooling` 前的 Activation Map 作为 __Style Loss__, 特定一层的 Activation Map 作为 __ConTent Loss__

![](../Img/2019-08-17/st2.png)

`VGG16` 的结构

```python
model = torchvision.models.vgg16(pretrained=True).features
print(model)
```

```Shell
Sequential(
  (0): Conv2d(3, 64, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
  (1): ReLU(inplace)
  (2): Conv2d(64, 64, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
  (3): ReLU(inplace)
  (4): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
  (5): Conv2d(64, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
  (6): ReLU(inplace)
  (7): Conv2d(128, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
  (8): ReLU(inplace)
  (9): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
  (10): Conv2d(128, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
  (11): ReLU(inplace)
  (12): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
  (13): ReLU(inplace)
  (14): Conv2d(256, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
  (15): ReLU(inplace)
  (16): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
  (17): Conv2d(256, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
  (18): ReLU(inplace)
  (19): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
  (20): ReLU(inplace)
  (21): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
  (22): ReLU(inplace)
  (23): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
  (24): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
  (25): ReLU(inplace)
  (26): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
  (27): ReLU(inplace)
  (28): Conv2d(512, 512, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1))
  (29): ReLU(inplace)
  (30): MaxPool2d(kernel_size=2, stride=2, padding=0, dilation=1, ceil_mode=False)
)
```

也就是说, 把编号 `3, 8, 15, 22` 的 __Feature Map__ 拿出来做 __Style Loss__, `15` 的 __Feature Map__ 做 __Content Loss__.

这里用 __Gram__ 矩阵衡量输入图像与风格图像的内容差异, 根据生成图像和风格图像在 __VGG16__ 不同阶段的特征图的 __Gram__ 矩阵之间的均方误差来优化生成图像和风格图像之间的风格差异.

```Python
def gram_matrix(y):
    (b, ch, h, w) = y.size()
    features = y.view(b, ch, w * h)
    features_t = features.transpose(1, 2)
    gram = features.bmm(features_t) / (ch * h * w)
    return gram
```

## Results
![wave](https://raw.githubusercontent.com/YinengXiong/YinengXiong.github.io/master/img/2019-08-17/concat_wave.png)

![picasso](https://raw.githubusercontent.com/YinengXiong/YinengXiong.github.io/master/img/2019-08-17/concat_picasso.png)

![mountainprism](https://raw.githubusercontent.com/YinengXiong/YinengXiong.github.io/master/img/2019-08-17/concat_mountainprism.png)

![scream](https://raw.githubusercontent.com/YinengXiong/YinengXiong.github.io/master/img/2019-08-17/concat_scream.png)

![vangogh](https://raw.githubusercontent.com/YinengXiong/YinengXiong.github.io/master/img/2019-08-17/concat_vangogh.png)

![edtaonisl](https://raw.githubusercontent.com/YinengXiong/YinengXiong.github.io/master/img/2019-08-17/concat_edtaonisl.png)

### 下期预告
CityScapes