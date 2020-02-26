# keras基础

## Windows环境配置
### 推荐配置
如果是高校学生或者高级研究人员，并且实验室或者个人资金充沛，建议您采用如下配置：
主板：X299型号或Z270型号
CPU: i7-6950X或i7-7700K 及其以上高级型号
内存：品牌内存，总容量32G以上，根据主板组成4通道或8通道
SSD： 品牌固态硬盘，容量256G以上
显卡：`NVIDIA GTX TITAN(XP)` 、`NVIDIA GTX 1080ti`、`NVIDIA GTX TITAN`、`NVIDIA GTX 1080`、`NVIDIA GTX 1070`、`NVIDIA GTX 1060` **(顺序为优先建议，并且建议同一显卡，可以根据主板插槽数量购买多块，例如X299型号主板最多可以采用×4的显卡)**
电源：由主机机容量的确定，一般有显卡总容量后再加200W即可

### CPU说明
大多数CPU目前支持多核多线程，那么如果您采用CPU加速，就可以使用多线程运算。这方面的优势对于服务器CPU Xeon系列尤为关键
### 显卡说明
如果您的显卡是非NVIDIA公司的产品或是NVIDIA GTX系列中型号的第一个数字低于6或NVIDIA的GT系列，都不建议您采用此类显卡进行加速计算，例如NVIDIA GT 910、NVIDIA GTX 460 等等。
如果您的显卡为**笔记本上的GTX移动显卡（型号后面带有标识M），那么请您慎重使用显卡加速，因为移动版GPU容易发生过热烧毁现象**。
如果您的显卡，显示的是诸如 HD5000,ATI 5650 等类型的显卡，那么您只能使用CPU加速
如果您的显卡芯片为Pascal架构（NVIDIA GTX 1080,NVIDIA GTX 1070等），您只能在之后的配置中选择CUDA 8.0

如果安装了tensorflow-gpu版，但是在测试时只想用cpu版本，可以作如下修改
```
import os
os.environ["CUDA_VISIBLE_DEVICES"]="-1"    
import tensorflow as tf
```

Keras如果是使用Theano后端的话，应该是自动不使用GPU只是用CPU的，启动GPU使用Theano内部命令即可。 
对于Tensorflow后端的Keras以及Tensorflow会自动使用可见的GPU，而我需要其必须只运行在CPU上。
网上查到三种方法，最后一种方法对我有用，但也对三种都做如下记录：
1. 使用tensorflow的 `with tf.device('/cpu:0')`:函数。简单操作就是把所有命令都放在前面所述的域里面。使用tensorflow声明Session时的参数： 对于Tensorflow，声明Session的时候加入`device_count={'gpu':0}`即可，代码如下:
```
import tensorflow as tf  
sess = tf.Session(config=tf.ConfigProto(device_count={'gpu':0}))
```

2. 对于Keras,则调用后端函数，设置其使用如上定义的Session即可，代码如下:

```
import tensorflow as tf
import keras.backend.tensorflow_backend as KTF
 
KTF.set_session(tf.Session(config=tf.ConfigProto(device_count={'gpu':0})))
```

3. 第三种是使用CUDA_VISIBLE_DEVICES命令行参数，代码如下：
```
CUDA_VISIBLE_DEVICES="0" python3 train.py
```