# HumanFallDetectionLSTM
利用 OpenPifPaf 对输入视频进行人体姿势估计,然后通过长短时记忆神经网络（LSTM）从前面得到的姿势信息中提取五个时间和空间特征以预测"跌倒"动作,支持多摄像头和多人实时检测。
## 检测实例见 examples 文件夹
## 安装

```shell script
pip install -r requirements.txt
```

## 使用
```shell script
python3 fall_detector.py --num_cams=1
```

## 参考
https://github.com/openpifpaf/openpifpaf