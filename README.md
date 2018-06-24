TensorFlow-GPU-
===============================
关于各版本的选择、安装(对应tensorflow版本，对应CUDA版本，对应cuDNN版本，对应英伟达驱动版本)、配置
-------------------------------

### 首先需要查看GPU的计算能力是否能够支持tensorflow-GPU版本，[各英伟达GPU计算能力一览](https://developer.nvidia.com/cuda-gpus)

### [接着查看Cuda各版本所需求的英伟达GPU驱动版本](https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html)

![image](https://github.com/HEIDIES/TensorFlow-GPU-/blob/master/tabel-one.png)

### 查看自己的GPU驱动版本
      $ nvidia-smi

### 如果想要安装CUDA最新版，[获取并下载自己的GPU的最新驱动](https://www.nvidia.cn/Download/index.aspx?lang=cn) ，但很操蛋的是，目前官网上linux的驱动最新的版本只有390.67

#### 安装英伟达GPU驱动：手动安装390.67,更改文件的执行权限 
      $ sudo chmod a+x NVIDIA-Linux-x86_64-390.67.run
      $ sudo gedit /etc/modprobe.d/blacklist.conf
   在最后一行后面添加：
   
      blacklist vga16fb
      blacklist nouveau
      blacklist rivafb
      blacklist rivatv
      blacklist nvidiafb
   删除原有驱动：
   
      $ sudo apt-get --purge remove nvidia-*
      $ sudo apt-get --purge remove xserver-xorg-video-nouveau
   按下CTRL+ALT+F1，进入第一控制台(CTRL+ALT+F7返回)，并登入(login as:root)
   密码可通过
   
      $ sudo root password
   来修改
   登入root账户后，运行：
   
      # sudo service lightdm stop
      # sudo ./NVIDIA-Linux-x86_64-390.67.run --no-x-check --no-nouveau-check --no-opengl-files
   一直OK，安装完成后
   
      # sudo reboot
   开机后，输入：
   
      $ nvidia-smi
   可以验证驱动安装成功了

#### 没办法，只能退而求其次的[选择CUDA9.1进行安装](https://developer.nvidia.com/cuda-toolkit-archive)，以及[选择下载相应的cuDNN](https://developer.nvidia.com/rdp/cudnn-archive)

![image](https://github.com/HEIDIES/TensorFlow-GPU-/blob/master/tabel-two.png)

   以CUDA9.1和cuDNN7.0.5(相比标准的cuda，它在一些常用的神经网络操作上进行了性能的优化，比如卷积，pooling，归一化，以及激活层等等。)为例。CUDA选择下载runfile文件，安装完成后，运行：
   
      $ sudo gedit ~/.bashrc
   在该文件最后加入以下两行并保存：
      
      export PATH=/usr/local/cuda-9.1/bin:$PATH  
      export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
   cuDNN解压完成后，运行：
   
      $ sudo cp cuDNN/cuda/include/cudnn.h /usr/local/cuda/include 
      $ sudo cp cuDNN/cuda/lib64/* /usr/local/cuda/lib64

### 下载安装Anaconda，使用[清华大学开源软件镜像站进行下载并配置镜像](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/),其中Anaconda3-4.3.0.1-Linux-x86_64.sh对应python3.6.0，Anaconda3-5.1.0-Linux-x86_64.sh对应python3.6.3，以Anaconda3-5.1.0为例，创建tensorflow虚拟环境：
      $ conda create --name=tensorflow -python=3.6.3
   激活虚拟环境：
   
      $ source activate tensorflow
   取消激活：
      
      $ source deactivate
   在激活的环境下安装tensorflow-gpu版本，由于目前最新tensorflow-1.8.0尚不支持cuda-9.0以上的版本，需手动下载[Linux可用的CUDA-9.1版tensorflow-1.6.0](https://github.com/mind/wheels/releases/tag/tf1.6-gpu-cuda91)，选择下载tensorflow-1.6.0-cp36-cp36m-linux_x86_64.whl。下载完成后到对应路径下，运行：
      
      $ pip install xxx.whl
   接下来，终于可以开始你的深度学习之旅了！！
