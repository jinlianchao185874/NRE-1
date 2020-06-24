# 实体关系抽取
本项目使用
+ python 3.6
+ pytorch 1.2.0

## 数据
由于给定的数据集没有进行标注，在有限的时间内只标注了少量数据，模型运行起来效果很差，所以先使用了标注好的数据集
数据使用的是网上开源的数据集
数据划分为三部分：训练集(1400)、验证集(300)、测试集(300)

下面为一条数据的形式：
```
梅葆玥	梅兰芳	父母 坎坷经历梅葆玥之家庭合影1961年，梅兰芳先生病逝，葆玥、葆玖姐弟俩继承父亲的遗志，挑起了梅剧团的重担
```
数据格式为: 实体1 实体2 关系 句子。

## 训练
模型主要目的是进行实体间关系的多分类任务。

模型使用的是lstm+attention模型。BiLSTM用于提取上下文信息，Attention用于得到句子级别的向量表示。

每个样本特征 :  pos1 + word + pos2 。其中pos1和pos2分别代表当前word对于实体1和实体2距离的向量表征。

数据集一共包含11中关系，可在relation2id.txt中查看

训练前先运行data文件夹中的 `data_util.py` 文件，将数据处理成pkl文件供模型使用。 

运行` main.py`即可开始训练，可以在`params_config.py`文件中设置epoch、batch等参数，运行结束模型会储存到backup文件夹中



## 准确率
自己电脑跑的一部分数据，结果如下，由于设置的epoch为10，所以三种参数值不是太高。
![result](https://github.com/jinlianchao185874/NRE-1/blob/master/result.jpg)



## 思考
加入其他的特征向量可能会提高准确率，论文中其他参数的设定是不是最优的，有待考证。

## 参考
Attention-Based Bidirectional Long Short-Term Memory Networks for Relation Classification

论文地址:https://www.aclweb.org/anthology/P16-2034/




