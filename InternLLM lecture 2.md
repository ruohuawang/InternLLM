1.部署 InternLM2-Chat-1.8B 模型核心步骤

（1）按需创建和配置开发机

可以根据使用场景对于GPU算力、显存的需求，按需开发机。本次申请10% A100 * 1即可用于微小规模训练。

镜像选用Cuda11.7-conda即可，GPU硬件的驱动决定了对于Cuda版本的支持。如需要更高版本的Cuda驱动，可能要升级底层GPU硬件驱动

（2）环境配置

studio-conda -o internlm-base -t demo

//studio-conda是定制化脚本或者集成开发环境（IDE）中封装的命令，可以简化对Conda环境的操作流程；

//基于一个基础环境模板internlm-base来新建一个名为demo的环境

或者等效配置方案

# conda create -n demo python==3.10 -y //使用conda命令创建一个名为demo的环境，并在其中安装确切版本为3.10的Python解释器，同时自动确认所有提示而无需用户交互

# conda activate demo //激活环境

# conda install pytorch==2.0.1 torchvision==0.15.2 torchaudio==2.0.2 pytorch-cuda=11.7 -c pytorch -c nvidia //在conda环境下安装特定版本的PyTorch相关库及其CUDA支持。（1）安装PyTorch版本为2.0.1（2）安装torchvision版本为0.15.2（是PyTorch的一个重要附加库，包含计算机视觉相关的数据集、模型和 transforms）（3）安装torchaudio版本为2.0.2（PyTorch的音频处理库）（4）安装与CUDA 11.7兼容的PyTorch版本，指定从PyTorch的官方频道（channel）下载并安装这些包，指定了另一个频道nvidia从中获取到与NVIDIA CUDA toolkit配合的优化版本或者其他与NVIDIA相关的软件包

（3）进入conda 环境，完成环境包的安装

conda activate demo //激活demo环境

pip install huggingface-hub==0.17.3

pip install transformers==4.34

pip install psutil==5.9.8

pip install accelerate==0.24.1

pip install streamlit==1.32.2

pip install matplotlib==3.8.3

pip install modelscope==1.9.5

pip install sentencepiece==0.1.99

（4）下载 InternLM2-Chat-1.8B 模型

按路径创建文件夹，并进入到对应文件目录中

mkdir -p /root/demo //make directory创建目录，-parents确保路径所有父目录都存在，即新建/root/demo目录

touch /root/demo/cli_demo.py //touch如果文件不存在，则会创建一个新文件

touch /root/demo/download_mini.py //新建一个空Python脚本文件

cd /root/demo //change directory” 的缩写，用于切换当前工作目录到指定位置
