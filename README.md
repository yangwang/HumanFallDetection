# 基于 OpenPifPaf 的多摄像头多人实时跌倒等异常行为识别预警应用研究
<p align="center">
<img src="documents/outfallingdown1.gif?raw=true" alt="outfallingdown"/>
<p align="center">
<img src="documents/outfallingdown2.gif?raw=true" alt="outfallingdown" style="zoom:90%;"/>


利用 OpenPifPaf 对输入视频进行人体姿势估计,然后通过长短时记忆神经网络（LSTM）从前面得到的姿势信息中提取五个时间和空间特征（作为当前的 *X*<sub>n</sub> 输入）以预测"跌倒"动作,支持多摄像头和多人实时检测。基于 PyTorch 在 UP-Fall Detection 数据集上训练，识别准确率达到 98.2% 。

<p align="center">
<img src="flowchart.png?raw=true" alt="LSTM" style="zoom:68%;" />
<p align="center">
<img src="LSTM.png?raw=true" alt="LSTM" style="zoom:45%;" />

## 安装
```shell script
pip install -r requirements.txt
```

## 使用
```shell script
python fall_detector.py --num_cams=1
```


## 完整运行代码

    usage: fall_detector.py [-h] [--seed-threshold SEED_THRESHOLD]
                            [--instance-threshold INSTANCE_THRESHOLD]
                            [--keypoint-threshold KEYPOINT_THRESHOLD]
                            [--decoder-workers DECODER_WORKERS]
                            [--dense-connections]
                            [--dense-coupling DENSE_COUPLING] [--caf-seeds]
                            [--no-force-complete-pose]
                            [--profile-decoder [PROFILE_DECODER]]
                            [--cif-th CIF_TH] [--caf-th CAF_TH]
                            [--connection-method {max,blend}] [--greedy]
                            [--checkpoint CHECKPOINT] [--basenet BASENET]
                            [--headnets HEADNETS [HEADNETS ...]] [--no-pretrain]
                            [--two-scale] [--multi-scale] [--no-multi-scale-hflip]
                            [--cross-talk CROSS_TALK] [--no-download-progress]
                            [--head-dropout HEAD_DROPOUT] [--head-quad HEAD_QUAD]
                            [--resolution RESOLUTION] [--resize RESIZE]
                            [--num_cams NUM_CAMS] [--video VIDEO] [--debug]
                            [--disable_cuda] [--plot_graph] [--joints]
                            [--skeleton] [--coco_points] [--save_output]
                            [--fps FPS] [--out-path OUT_PATH]
                            [--input_direct INPUT_DIRECT]
    
    optional arguments:
      -h, --help            show this help message and exit
      --resolution RESOLUTION
                            Resolution prescale factor from 640x480. Will be
                            rounded to multiples of 16. (default: 0.4)
      --resize RESIZE       Force input image resize. Example WIDTHxHEIGHT.
                            (default: None)
      --num_cams NUM_CAMS   Number of Cameras. (default: 1)
      --video VIDEO         Path to the video file. For single video fall
                            detection(--num_cams=1), save your videos as abc.xyz
                            and set --video=abc.xyz For 2 video fall
                            detection(--num_cams=2), save your videos as abc1.xyz
                            & abc2.xyz and set --video=abc.xyz (default: None)
      --debug               debug messages and autoreload (default: False)
      --disable_cuda        disables cuda support and runs from gpu (default:
                            False)
    
    decoder configuration:
      --seed-threshold SEED_THRESHOLD
                            minimum threshold for seeds (default: 0.5)
      --instance-threshold INSTANCE_THRESHOLD
                            filter instances by score (default: 0.2)
      --keypoint-threshold KEYPOINT_THRESHOLD
                            filter keypoints by score (default: None)
      --decoder-workers DECODER_WORKERS
                            number of workers for pose decoding (default: None)
      --dense-connections   use dense connections (default: False)
      --dense-coupling DENSE_COUPLING
                            dense coupling (default: 0.01)
      --caf-seeds           [experimental] (default: False)
      --no-force-complete-pose
      --profile-decoder [PROFILE_DECODER]
                            specify out .prof file or nothing for default file
                            name (default: None)
    
    CifCaf decoders:
      --cif-th CIF_TH       cif threshold (default: 0.1)
      --caf-th CAF_TH       caf threshold (default: 0.1)
      --connection-method {max,blend}
                            connection method to use, max is faster (default:
                            blend)
      --greedy              greedy decoding (default: False)
    
    network configuration:
      --checkpoint CHECKPOINT
                            Load a model from a checkpoint. Use "resnet50",
                            "shufflenetv2k16w" or "shufflenetv2k30w" for
                            pretrained OpenPifPaf models. (default: None)
      --basenet BASENET     base network, e.g. resnet50 (default: None)
      --headnets HEADNETS [HEADNETS ...]
                            head networks (default: None)
      --no-pretrain         create model without ImageNet pretraining (default: True)
      --two-scale           [experimental] (default: False)
      --multi-scale         [experimental] (default: False)
      --no-multi-scale-hflip
                            [experimental] (default: True)
      --cross-talk CROSS_TALK
                            [experimental] (default: 0.0)
      --no-download-progress
                            suppress model download progress bar (default: True)
    
    head:
      --head-dropout HEAD_DROPOUT
                            [experimental] zeroing probability of feature in head
                            input (default: 0.0)
      --head-quad HEAD_QUAD
                            number of times to apply quad (subpixel conv) to heads
                            (default: 1)
    
    Visualisation:
      --plot_graph          Plot the graph of features extracted from keypoints of
                            pose. (default: False)
      --joints              Draw joints keypoints on the output video. (default: True)
      --skeleton            Draw skeleton on the output video. (default: True)
      --coco_points         Visualises the COCO points of the human pose. (default: False)
      --save_output         Save the result in a video file. Output videos are
                            saved in the same directory as input videos with "out"
                            appended at the start of the title (default: False)
      --fps FPS             FPS for the output video. (default: 18)
      --out-path OUT_PATH   Save the output video at the path specified. .avi file
                            format. (default: result.avi)
      --input_direct INPUT_DIRECT
                            Save the input link to images directory. (default: None)
- 模型输入可以直接为摄像头作为视频源或者用下载好的视频作为视频源。
- 如果在非服务器端可以通过设置在窗口进行实时画面的显示。

## 参考
- [OpenPifPaf](https://github.com/openpifpaf/openpifpaf)
- [UP-fall detection Dataset](https://dx.doi.org/10.3390/s19091988)
- [Multi-camera, multi-person, and real-time fall detection using long short term memory](https://doi.org/10.1117/12.2580700)
- Lei Wang, Du Q. Huynh, Piotr Koniusz. A Comparative Review of Recent Kinect-based Action Recognition Algorithms[J]. IEEE TRANSACTIONS ON IMAGE PROCESSING,2019.
- Nusrat Tasnim , Mohammad Khairul Islam and Joong-Hwan Baek. Deep Learning Based Human Activity Recognition Using Spatio-Temporal Image Formation of Skeleton Joints[J].applied sciences.
- Mickael Delamare, Cyril Laville, Adnane Cabani and Houcine Chafouk. Graph Convolutional Networks Skeleton-based Action Recognition for Continuous Data Stream: A Sliding Window Approach[J]. 16th International Conference on Computer Vision Theory and Applications.
- Tasweer Ahmad, Lianwen Jin, Xin Zhang, Songxuan Lai, Guozhi Tang, and Luojun Lin. Graph Convolutional Neural Network for Human Action Recognition: A Comprehensive Survey[J].
- Zehua Sun, Jun Liu, Qiuhong Ke, Hossein Rahmani, Mohammed Bennamoun, and Gang Wang. Human Action Recognition from Various Data Modalities: A Review[J].
