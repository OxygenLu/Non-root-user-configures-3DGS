# Non-root-user-configures-3DGS
## 创建虚拟环境并下载 

```Bash
conda create -n gs python==3.10
git clone https://github.com/graphdeco-inria/gaussian-splatting.git

```

## 检查cuda环境

```Bash
nvcc -V
# 需要和torch的cuda安装版本对应
# 如果不对应需要升级

```

查看一下conda中能下载的cuda-nvcc环境

```Bash
conda search -c nvidia cuda-nvcc
conda install -c nvidia cuda-nvcc==12.4
# 本文以12.4的cuda-torch为例子

```

安装torch

```Bash
# 激活环境
conda activate gs
# 12.4
pip install torch==2.6.0 torchvision==0.21.0 torchaudio==2.6.0 --index-url https://download.pytorch.org/whl/cu124
# 指定一下你的CUDA_HOME
export CUDA_HOME=/usr/local/cuda


```

安装diff-gaussian-rasterization和simple-knn

如果出现erro，如下：

```Bash
error: #error "You're trying to build PyTorch with a too old version of GCC. We need GCC 9 or later."
```

太旧了就更新，太新了就降低

```Bash
# 在 conda 环境中安装 GCC 11
conda install -c conda-forge gxx_linux-64=11.2.0 gcc_linux-64=11.2.0
# 指定CC的环境路径
export CC=/usr/bin/gcc-9


```

记得要清空一下之前编译失败的缓存

```Bash
cd submodules/diff-gaussian-rasterization
rm -rf build/ dist/ *.egg-inf
cd ../..
pip install ./submodules/diff-gaussian-rasterization

# 再次查看一遍gcc版本
gcc --version
g++ --version
nvcc -V

echo $PATH
export PATH=$CONDA_PREFIX/bin:$PATH


```

```Bash
cd submodules/diff-gaussian-rasterization
rm -rf build/ dist/ *.egg-inf
cd ../..
pip install ./submodules/diff-gaussian-rasterization

# 再次查看一遍gcc版本
gcc --version
g++ --version
nvcc -V

echo $PATH
export PATH=$CONDA_PREFIX/bin:$PATH


```

```Bash
#开始编译
pip install ./submodules/diff-gaussian-rasterization
pip install ./submodules/simple-knn/

```

## Training

```Bash
python train.py -s dataset/ -m dataset/output -w
```
