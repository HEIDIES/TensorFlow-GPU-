# TensorFlow-GPU-
===============================
关于各版本的选择、安装(对应tensorflow版本，对应CUDA版本，对应cuDNN版本，对应英伟达驱动版本)、配置
-------------------------------

##首先需要查看GPU的计算能力是否能够支持tensorflow-GPU版本，各英伟达GPU计算能力一览 [This link]https://developer.nvidia.com/cuda-gpus

##接着查看Cuda各版本所需求的英伟达GPU驱动版本 https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html

![image](https://github.com/HEIDIES/TensorFlow-GPU-/blob/master/tabel-one.png)

##可以通过 https://www.nvidia.cn/Download/index.aspx?lang=cn 获取并下载自己的GPU的最新驱动，但很操蛋的是，目前官网上linux的驱动最新的版本只有390.67

###

没办法，只能退而求其次的选择CUDA9.1进行安装，相应的cuDNN https://developer.nvidia.com/rdp/cudnn-archive 

![image](https://github.com/HEIDIES/TensorFlow-GPU-/blob/master/tabel-two.png)

