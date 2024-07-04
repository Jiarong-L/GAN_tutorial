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

* [SHAP](https://shap.readthedocs.io/en/latest/index.html) 尝试见 'Basis_PyTorch.ipynb'

* 图像GAN的评价指标
    - Inception Score：将生成图像输入预训练好的Inception-v3模型，更**真实**图像的分类概率比较集中(e.g.[0.9999,0.00001,0,0,0,0,...])；而图像类别的分布均匀与否也可以反应**多样性**
    - FID：提取真实样本（也使用Inception-v3模型）、生成样本的分布参数，计算两个分布之间的距离


* 很容易[模式崩溃](https://aiden.nibali.org/blog/2017-01-18-mode-collapse-gans/)
    - mini-batch & small-lr 似乎都没啥用
    - 尝试引入一些错误label？？？
    - **隔几步就返回用旧的D**_ok
    - 给G更多randomness_ok
    - 限制D的参数不要超过某个常数（weight clipping），此时不推荐SGD/momentum/Adam，推荐RMSprop（适合梯度不稳定的情况）

* 判别器过强可能导致生成器只能持续生成噪音（Generator Loss 上升，Discriminator Loss 下降）；但生成器也可能生成无意义但可以欺骗判别器的图像（Discriminator Loss 上升）：需要给生成器多一些训练步骤 / 加大生成器 learning rate 

* 注意激活函数的取值范围，注意 FakeImgs 与 RealImgs 的取值范围应一致, e.g. [0,1] or [0,255] or [-1,1]

* 评价生成图片与真实图片之间的距离：JS散度对于距离较远的情况无能为力，此时推荐使用Wasserstein距离（wGAN+RMSprop）
    - ```lossfnD = tf.reduce_mean(descR)-tf.reduce_mean(descF)``` 
    - ```lossfnG = -tf.reduce_mean(descF)```
    - descR指D对Realimg的判别结果

* semi-supervised GAN：将multi-head输出[0,1]+[c1,c2,c3]合并成[Fake,c1,c2,c3]，如此可以利用无标签的真实图像

* Generative models 不只有 GAN，还可以用 RL 等方式优化 decoder

* [register_buffer()](https://blog.csdn.net/weixin_46197934/article/details/119518497)

### Readings

Pytorch: https://pytorch.org/tutorials/    
lr_schedule: https://zhuanlan.zhihu.com/p/465097436   
FBGAN: https://zhuanlan.zhihu.com/p/71741284     



### Version Compatibility

注意版本 Compatibility: torch & torchvision & [torchtext](https://pypi.org/project/torchtext/)& [torchaudio](https://pytorch.org/audio/main/installation.html#compatibility-matrix)，否则会卸载torch后自动安装cpu版本
```bash
pip install torch==2.2.0  --index-url https://download.pytorch.org/whl/cu121
pip install torchtext==0.17.0  portalocker
pip install torchvision==0.17.0
pip install torchaudio==2.2.0
pip install torch-scatter torch-sparse torch-cluster -f https://data.pyg.org/whl/torch-2.2.0+cpu.html
# pip install torch-spline-conv 
pip install torch-geometric

           py:3.11.9
torch                     2.2.0+cu121
torchaudio                2.2.0
torchdata                 0.7.1
torchtext                 0.17.0
torchvision               0.17.0
```




