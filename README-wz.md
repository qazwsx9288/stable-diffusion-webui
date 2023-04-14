### 环境配置

#### 安装问题

程序要求python是3.9，安装使用的版本为3.9.13

#### 安装流程

确保你的显卡驱动支持cuda117，如果你的windows有多个cuda，使用环境变量来控制版本。

安装cuda
cuda_11.7.1_516.94_windows.exe

安装cudnn
cudnn-windows-x86_64-8.8.0.121_cuda11-archive.zip
解压后复制到cuda的安装目录
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.7

配置cuda的环境变量
系统属性-环境变量-系统变量-找到Path点击编辑
确保以下环境变量都存在
```
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.7\bin
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.7\libnvvp
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.7\lib
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.7\include
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.7\extras\CUPTI\lib64
```

pytorch 下载站
https://download.pytorch.org/whl/cu117/torch/
这是具体已找到的地址，可用迅雷或aria2下载
https://download.pytorch.org/whl/cu117/torch-1.13.0%2Bcu117-cp39-cp39-win_amd64.whl
https://download.pytorch.org/whl/cu117/torchvision-0.14.1%2Bcu117-cp39-cp39-win_amd64.whl


双击执行webui-user.bat 直到它开始安装torch时，强制结束，并在vscode中打开本项目。
这一步主要是为了在项目目录创建venv的python环境，此环境的python版本取决于系统python的版本。

在vscode打开控制台，此时控制台会提示环境为(venv)
分别安装之前下载好的2个离线包，例如离线包位置在桌面：

```bash
pip install C:\\Users\\Administrator\\Desktop\\torchvision-0.14.1+cu117-cp39-cp39-win_amd64.whl
```

安装好之后，双击执行webui-user.bat继续安装其他依赖。
也可以在控制台，直接执行launch.py
```bash
python .\launch.py
```
此时有可能会出现git clone 或者 git fetch时的错误，不需要管，重新反复执行直到安装完毕即可。

程序会先去github克隆很多项目作为依赖

然后会安装然后会安装 requirements 依赖

安装完成之后，会检查是否有这个模型文件在项目中
`\models\Stable-diffusion\v1-5-pruned-emaonly.safetensors`

如果没有，程序就会自动下载，这个下载无法断点续传。建议用其他软件下载完成之后，再放到目录中。下载地址：
https://huggingface.co/runwayml/stable-diffusion-v1-5/resolve/main/v1-5-pruned-emaonly.safetensors



在webui-user.bat中配置COMMANDLINE_ARGS
双击执行：
webui-user.bat

在vscode中执行：
需要注意的是这样执行的话，`webui-user.bat`的配置都无效了，需要手动在命令中添加参数
```bash
python launch.py --xformers
```

如果没有安装xformers，需要手动安装。特别是python3.9，程序校验到3.9是不会自动安装xformers的
```bash
pip install -U -I --no-deps xformers==0.0.16rc425
```