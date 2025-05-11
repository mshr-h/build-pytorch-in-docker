# build-pytorch-in-docker
[WIP] Build and Develop PyTorch with Docker

```bash
uv venv --python 3.11
git clone --recursive https://github.com/pytorch/pytorch
source .venv/bin/activate
cd pytorch
uv pip install -r requirements.txt setuptools cython cmake ninja
export CMAKE_C_COMPILER_LAUNCHER=ccache
export CMAKE_CXX_COMPILER_LAUNCHER=ccache
export CMAKE_CUDA_COMPILER_LAUNCHER=ccache
USE_CUDA=1 python setup.py develop

cd ../
git clone --recursive https://github.com/pytorch/vision
cd vision
USE_CUDA=1 python setup.py develop

cd ../
git clone --recursive https://github.com/apache/tvm
cd tvm
cmake -S . -B build -G Ninja -DUSE_MLIR=ON -DUSE_CPP_RPC=ON -DUSE_MSC=ON -DUSE_LLVM=llvm-config-19
cmake --build build
uv pip install -e python --config-setting editable-mode=compat
```
