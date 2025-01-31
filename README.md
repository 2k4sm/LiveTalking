# Real-time Interactive Streaming Digital Human

Real-time interactive streaming digital human enables synchronized audio-video dialogue, achieving near-commercial effects.

[ernerf Effect](https://www.bilibili.com/video/BV1PM4m1y7Q2/)  [musetalk Effect](https://www.bilibili.com/video/BV1gm421N7vQ/)  [wav2lip Effect](https://www.bilibili.com/video/BV1Bw4m1e74P/)

## To avoid confusion with 3D digital humans, the original project "metahuman-stream" has been renamed to "livetalking." The original link remains available.

## News
- 2024.12.8 Improved multi-concurrency, VRAM usage does not increase with the number of concurrent instances.
- 2024.12.21 Added preloading for wav2lip and musetalk models to resolve the initial inference lag. Thanks to @heimaojinzhangyz
- 2024.12.28 Added the Ultralight-Digital-Human model. Thanks to @lijihua2017
- 2025.1.26 Added the wav2lip384 model. Thanks to @NotDumbNotDumb

## Features
1. Supports multiple digital human models: ernerf, musetalk, wav2lip, Ultralight-Digital-Human
2. Supports voice cloning
3. Supports interruption while the digital human is speaking
4. Supports full-body video stitching
5. Supports RTMP and WebRTC
6. Supports video orchestration: plays a custom video when not speaking
7. Supports multi-concurrency

## 1. Installation

Tested on Ubuntu 20.04, Python 3.10, PyTorch 1.12, and CUDA 11.3

### 1.1 Install Dependencies

```bash
conda create -n nerfstream python=3.10
conda activate nerfstream
# If CUDA version is not 11.3 (check using `nvidia-smi`), install the corresponding version of PyTorch from <https://pytorch.org/get-started/previous-versions/>
conda install pytorch==1.12.1 torchvision==0.13.1 cudatoolkit=11.3 -c pytorch
pip install -r requirements.txt
# If you do not need to train the ernerf model, you do not need to install the following libraries
pip install "git+https://github.com/facebookresearch/pytorch3d.git"
pip install tensorflow-gpu==2.8.0
pip install --upgrade "protobuf<=3.20.1"
```
Common installation issues: [FAQ](https://livetalking-doc.readthedocs.io/en/latest/faq.html)  
For setting up the Linux CUDA environment, refer to this article: https://zhuanlan.zhihu.com/p/674972886

## 2. Quick Start

- Download the models  
Baidu Cloud: <https://pan.baidu.com/s/1yOsQ06-RIDTJd3HFCw4wtA> Password: ltua  
Google Drive: <https://drive.google.com/drive/folders/1FOC_MD6wdogyyX_7V1d4NDIO7P9NlSAJ?usp=sharing>  
Copy `wav2lip384.pth` to the `models` folder of this project and rename it to `wav2lip.pth`.  
Extract `wav2lip384_avatar1.tar.gz`, and copy the entire folder to `data/avatars` within this project.

- Run the program  
```bash
python app.py --transport webrtc --model wav2lip --avatar_id wav2lip384_avatar1  
```
Open `http://serverip:8010/webrtcapi.html` in your browser, enter any text in the text box, and submit. The digital human will read the entered text.

<font color=red>The server needs to open the following ports: TCP:8010; UDP:1-65536</font>

If you cannot access Hugging Face, run the following command before starting:
```bash
export HF_ENDPOINT=https://hf-mirror.com
```

## 3. More Usage

Usage Guide: <https://livetalking-doc.readthedocs.io/>

## 4. Docker Run  

No need for prior installation, just run the following command:
```bash
docker run --gpus all -it --network=host --rm registry.cn-beijing.aliyuncs.com/codewithgpu2/lipku-metahuman-stream:vjo1Y6NJ3N
```
The code is located in `/root/metahuman-stream`. First, run `git pull` to fetch the latest code, then follow the commands from steps 2 and 3.

Available Docker images:
- AutoDL Image: <https://www.codewithgpu.com/i/lipku/metahuman-stream/base>  
[AutoDL Tutorial](https://livetalking-doc.readthedocs.io/en/latest/autodl/README.html)
- UCloud Image: <https://www.compshare.cn/images-detail?ImageID=compshareImage-16ktl2kxwjef&ImageType=Community&referral_code=3XW3852OBmnD089hMMrtuU&ytag=lipku_github>  
Supports opening any port, no need to deploy the SRS service separately.  
[UCloud Tutorial](https://livetalking-doc.readthedocs.io/en/latest/ucloud/ucloud.html)

## 5. TODO
- [x] Add ChatGPT to enable digital human conversations
- [x] Voice cloning
- [x] Replace silent periods with a video
- [x] MuseTalk
- [x] Wav2Lip
- [x] Ultralight-Digital-Human

---
If this project is helpful to you, please consider giving it a star. Contributions are also welcome!

* Knowledge Planet: https://t.zsxq.com/7NMyO - Contains high-quality FAQs, best practices, and problem solutions.  
* WeChat Official Account: "Digital Human Technology"  
![WeChat QR Code](https://mmbiz.qpic.cn/sz_mmbiz_jpg/l3ZibgueFiaeyfaiaLZGuMGQXnhLWxibpJUS2gfs8Dje6JuMY8zu2tVyU9n8Zx1yaNncvKHBMibX0ocehoITy5qQEZg/640?wxfrom=12&tp=wxpic&usePicPrefetch=1&wx_fmt=jpeg&amp;from=appmsg)

