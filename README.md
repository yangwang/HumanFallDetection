# 基于 OpenPifPaf 的多摄像头、多人实时跌倒检测模型
<p align="center">
<img src="https://git.trustie.net/pkwhiuqat/HumanFallDetectionLSTM/raw/branch/master/examples/outfallingdown.gif?raw=true" alt="outfallingdown"/>

利用 OpenPifPaf 对输入视频进行人体姿势估计,然后通过长短时记忆神经网络（LSTM）从前面得到的姿势信息中提取五个时间和空间特征（作为当前的 *X*<sub>n</sub> 输入）以预测"跌倒"动作,支持多摄像头和多人实时检测。模型在 UP-Fall Detection 数据集上训练，基于 PyTorch 实现。

<p align="center">
<img src="https://git.trustie.net/pkwhiuqat/HumanFallDetectionLSTM/raw/branch/master/flowchart.png?raw=true" alt="LSTM" style="zoom:68%;" />
<p align="center">
<img src="https://git.trustie.net/pkwhiuqat/HumanFallDetectionLSTM/raw/branch/master/LSTM.png?raw=true" alt="LSTM" style="zoom:45%;" />

## 安装
```shell script
pip install -r requirements.txt
```

## 使用
```shell script
python fall_detector.py --num_cams=1
```

# Alphapose部分说明

## Alphapose介绍

AlphaPose采用自顶向下的方法，提出了RMPE（区域多人姿态检测）框架。该框架主要包括symmetric spatial transformer network (SSTN)、Parametric Pose Non- Maximum-Suppression (NMS)和Pose-Guided Proposals Generator (PGPG)。并且使用symmetric spatial transformer network (SSTN)、deep proposals generator (DPG) 、parametric pose nonmaximum suppression (p-NMS) 三个技术来解决野外场景下多人姿态估计问题。

在SPPE结构上添加SSTN，能够在不精准的区域框中提取到高质量的人体区域。并行的SPPE分支（SSTN）来优化自身网络。使用parametric pose NMS来解决冗余检测问题，在该结构中，使用了自创的姿态距离度量方案比较姿态之间的相似度。用数据驱动的方法优化姿态距离参数。最后我们使用PGPG来强化训练数据，通过学习输出结果中不同姿态的描述信息，来模仿人体区域框的生成过程，进一步产生一个更大的训练集。

## Alphapose在该项目的作用

可以向Alphapose输入人体行为视频，输出.avi格式的附带人体骨架的视频，这种视频或许可以用来作为OpenPifPaf的输入素材使用。

## Alphapose项目运行环境

pytorch1.4

cuda10.1

cudnn7

ubuntu18.04

## Alphapose配置步骤

1、在命令提示符里输入cuda的路径。

export PATH=/usr/local/cuda/bin/:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64/:$LD_LIBRARY_PATH

2、之后输入pip install .安装配置文件

## Alphapose使用流程

1、将视频存入特定文件夹，并记下视频路径。（建议存储在AlphaPose/data里面）

2、在命令提示符里输入如下内容运行Alphapose：

bash ./scripts/inference.sh configs/coco/resnet/256x192_res152_lr1e-3_1x-duc.yaml pretrained_models/fast_res50_256x192.pth 视频路径 outputs

3、在AlphaPose/outputs文件夹里找到输出的内容

注：若outputs文件夹里只生成了.json文件，则用记事本打开scripts/inference.sh，将里面最后一行的“#--save_video”中的“#”删除，之后再执行第二步即可。

## 参考
- [OpenPifPaf](https://github.com/openpifpaf/openpifpaf)
- [UP-fall detection Dataset](https://dx.doi.org/10.3390/s19091988)
- [Multi-camera, multi-person, and real-time fall detection using long short term memory](https://doi.org/10.1117/12.2580700)
- [AlphaPose](https://github.com/MVIG-SJTU/AlphaPose)