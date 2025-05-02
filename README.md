# build-pytorch-in-docker
[WIP] Build and Develop PyTorch with Docker

```bash
git clone --recursive https://github.com/pytorch/pytorch
uv pip install setuptools
source .venv/bin/activate
cd pytorch
uv pip install -r requirements
USE_CUDA=1 python setup.py develop

cd ../
git clone --recursive https://github.com/pytorch/vision
cd vision
USE_CUDA=1 python setup.py develop
```
