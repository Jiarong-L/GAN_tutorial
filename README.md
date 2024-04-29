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


很容易崩。。。


### Readings

Pytorch: https://pytorch.org/tutorials/    
FBGAN: https://zhuanlan.zhihu.com/p/71741284     







