Real time interactive streaming digital human， realize audio video synchronous dialogue. It can basically achieve commercial effects.  


## Features
1. Support for multiple digital human models: ernerf (or musetalk, wav2lip )  
2. Support voice cloning  
3. Support interruptions while the digital human is speaking  
4. Support full-body video stitching  
5. Support RTMP and WebRTC  
6. Support video orchestration: play custom videos when not speaking  
7. Support multiple concurrent operations

## 1. Installation

Tested on Ubuntu 20.04, Python3.10, Pytorch 1.12 and CUDA 11.3

### 1.1 Install dependency
```bash
conda create -n nerfstream python=3.10
conda activate nerfstream
conda install pytorch==1.12.1 torchvision==0.13.1 cudatoolkit=11.3 -c pytorch
pip install -r requirements.txt

pip install "git+https://github.com/facebookresearch/pytorch3d.git"
pip install tensorflow-gpu==2.8.0
pip install --upgrade "protobuf<=3.20.1"
```
## 2. Quick Start

```bash
export CANDIDATE='<ip>'  
docker run --rm --env CANDIDATE=$CANDIDATE \
  -p 1935:1935 -p 8080:8080 -p 1985:1985 -p 8000:8000/udp \
  registry.cn-hangzhou.aliyuncs.com/ossrs/srs:5 \
  objs/srs -c conf/rtc.conf
```

```python
python app.py
```

If you can't access HuggingFace, run it before
```
export HF_ENDPOINT=https://hf-mirror.com
```

Open the http://<serverip>:8010/rtcpushapi.html in a browser, enter any text in the text box, and submit. The digital human broadcasts the text  
Note: The server needs to open port tcp: 8000, 8010, 1985; udp:8000
---