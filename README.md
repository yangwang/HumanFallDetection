# 基于 OpenPifPaf 的多摄像头、多人实时跌倒检测模型
<p align="center">
<img src="https://git.trustie.net/pkwhiuqat/HumanFallDetectionLSTM/raw/branch/master/documents/outfallingdown.gif?raw=true" alt="outfallingdown"/>

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

## 参考
- [OpenPifPaf](https://github.com/openpifpaf/openpifpaf)
- [UP-fall detection Dataset](https://dx.doi.org/10.3390/s19091988)
- [Multi-camera, multi-person, and real-time fall detection using long short term memory](https://doi.org/10.1117/12.2580700)