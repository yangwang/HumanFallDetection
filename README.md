# HumanFallDetectionLSTM
我们通过支持多摄像头和多人跟踪以及长短时记忆（LSTM）神经网络来增强人体姿势估计（openpifpaf库），以预测两个类别。"跌倒 "或 "没有跌倒"。我们从姿势中提取五个时间和空间特征，由LSTM分类器处理。
## 检测实例见 examples 文件夹
## 安装

```shell script
pip install -r requirements.txt
```

## 使用
```shell script
python3 fall_detector.py --num_cams=1
```