# Anaconda-install-PyTorch-with-CUDA-on-Mac


## Configuration
- Mac OS X: 10.13.5 (OSX >= 10.14 does not support CUDA)
- GPU: GTX 1060 6GB
- CUDA: 9.1 
- cuDNN: v7.0.5 
- Python: 3.6


## Build PyTorch with CUDA in Anaconda environment step by step
0. assume you already install Anaconda
```
create an Anaconda environment
conda create --name ptc python=3.6 pip
conda activate ptc3
conda install numpy pyyaml mkl mkl-include setuptools cmake cffi typing
```

1. get PyTorch 1.0.0 (higher PyTorch does not work)
```
git clone --branch v1.0.0 https://github.com/pytorch/pytorch.git pytorch-1.0.0
git submodule update --init --recursive
```

2. compile and install PyTorch
```
cd pytorch-1.0.0
export CMAKE_PREFIX_PATH=~/anaconda3/envs/ptc3
MACOSX_DEPLOYMENT_TARGET=10.9 CC=clang CXX=clang++ python setup.py install
```

3. install jupyter notebook in the conda environment
```
conda install ipython jupyter notebook matplotlib
```

4. install torchvision
```
conda install torchvision --no-deps -c soumith 
or
pip install torchvision
```

5. restart your computer and activate conda environment
```
conda activate ptc3
```

6. test if you install successfully
```
python
import torch
torch.cuda.is_available()
If your output is "True", then you install correctly.
```


## Problems encountered 
1. When I run python -> import torch, I got the error: ModuleNotFoundError: No module named 'torch._C' 
but then I open jupyter notebook, run "import torch -> torch.cuda.is_available()" and it successes, so I ignore the error.

2. When I run python -> import torch -> torch.cuda.is_available(), it returns "True", but when I run the same code in jupyter notebook, it returns "False", that means I didn't install jupyter notebook correctly, so I re-run "conda install ipython jupyter notebook matplotlib" again.

3. I got my jupyter notebook run correctly and I can use PyTorch with CUDA, but when I install several libs like cv2, scipy, and sklearn, the cuda is out again. So I re-run step 2 again, and by careful, do not use pip install in your conda environment, it could mess up your configuration.
