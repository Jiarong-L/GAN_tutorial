# GAN_tutorial
Self-tutorials of Generative Models

```
Generator: Fake_imgs
                     \
                      Discriminator: 0/1
                     /
           Real_imgs
```

$\min\limits_G\max\limits_D V(D,G) = E_{x \sim p_{data}(x)}[\log D(x)] + E_{z \sim p_{z}(z)}[\log (1-D(G(z)))]$



D希望区分Fake/Real（最大化V），而G希望混淆D的判断（最小化V）


### Tips

* 很容易[模式崩溃](https://aiden.nibali.org/blog/2017-01-18-mode-collapse-gans/)。。。mini-batch & small-lr 似乎都没啥用，尝试引入一些错误label？？？**隔几步就返回用旧的D**_ok

* 判别器过强可能导致生成器只能持续生成噪音（Generator Loss 上升，Discriminator Loss 下降）；但生成器也可能生成无意义但可以欺骗判别器的图像（Discriminator Loss 上升）：需要给生成器多一些训练步骤 / 加大生成器 learning rate

* 注意激活函数的取值范围，注意 FakeImgs 与 RealImgs 的取值范围应一致, e.g. [0,1] or [0,255] or [-1,1]

* Generative models 不只有 GAN，还可以用 RL 等方式优化 decoder


### Readings

Pytorch: https://pytorch.org/tutorials/    
lr_schedule: https://zhuanlan.zhihu.com/p/465097436   
FBGAN: https://zhuanlan.zhihu.com/p/71741284     







