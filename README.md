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


很容易[模式崩溃](https://aiden.nibali.org/blog/2017-01-18-mode-collapse-gans/)。。。mini-batch & small-lr 似乎都没啥用，尝试引入一些错误label？？？**隔几步就返回用旧的D**_ok


### Readings

Pytorch: https://pytorch.org/tutorials/    
lr_schedule: https://zhuanlan.zhihu.com/p/465097436   
FBGAN: https://zhuanlan.zhihu.com/p/71741284     







