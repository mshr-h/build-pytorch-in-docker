# build-pytorch-in-docker
[WIP] Build and Develop PyTorch with Docker

```bash
git clone --recursive https://github.com/pytorch/pytorch
source .venv/bin/activate
cd pytorch
uv pip install -r requirements.txt setuptools
export CMAKE_C_COMPILER_LAUNCHER=ccache
export CMAKE_CXX_COMPILER_LAUNCHER=ccache
export CMAKE_CUDA_COMPILER_LAUNCHER=ccache
USE_CUDA=1 python setup.py develop

cd ../
git clone --recursive https://github.com/pytorch/vision
cd vision
USE_CUDA=1 python setup.py develop
```
