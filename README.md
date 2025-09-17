# KOCCA-3D Edit & CLIP-DS Evaluation 

이 프로젝트는 <b>3D 오브젝트(예: 3D-FUTURE)</b>를 대상으로

1) 이미지 캡셔닝(BLIP) → 
2) 객체 타입 추출 → 
3) 프롬프트 기반 참조 이미지 생성(HunyuanDiT) →  
4) 3D 텍스처링(Hunyuan3D) → 
5) CLIP Directional Similarity로 품질 평가 를 **배치로 자동화**

- 객체 생성 메인 스크립트: `run_batch_processing.py`  
- 객체 평가 유틸(모듈화): `evaluate_clip_ds.py` (함수/클래스 import)

---

## 0) Environments

- OS: Ubuntu 20.04
- GPU: NVIDIA-RTX-A5000 (VRAM 24GB)
- CUDA: 12.4
- Pytorch: 2.6.0 
- Network: Download Hugging Face model/pipeline at the first time

---

## 1) Repository Clone

```bash
git clone https://github.com/KAIST-VML/KOCCA-3DEdit.git
cd KOCCA-3DEdit
```

<br>

## 2) Setting Up the Environment
```bash
conda create -n kocca3d python=3.10 -y
conda activate kocca3d
```

```bash
# CUDA 12.4
pip install torch==2.6.0 torchvision==0.21.0 torchaudio==2.6.0 --index-url https://download.pytorch.org/whl/cu124
```

```bash
pip install -r requirements.txt
```

(optional)if you want to check requirements are installed well,
```bash
python pkg_check.py
```

please install sub-modules
```bash
# for texture
cd hy3dgen/texgen/custom_rasterizer
python3 setup.py install
cd ../../..
cd hy3dgen/texgen/differentiable_renderer
python3 setup.py install
cd ../../..
```


install xvfb-run (only gpu linux server like vessl required)
```bash
apt-get update
apt-get install -y \
    xvfb \
    freeglut3-dev \
    libgl1-mesa-glx \
    libglib2.0-0 \
    libosmesa6-dev \
    libglu1-mesa-dev
```

<br>

## 3) Prepare dataset
- KAIST VML Vessl sever **charater-s01**: /data2/hyeonseung/dataset/


## 4) Edited Object Generation
 

Theme list (10)
- art_deco
- bioluminescent
- claymation
- cyberpunk
- ghibli
- glass
- medieval
- steampunk
- wooden
- yellow


<br> 

```bash
xvfb-run --auto-servernum python run_batch_processing.py
```
=> The results are saved in /outputs_batch
<br> we have 8 files per objects.
<br>
- edited_mesh.glb
- editing_prompt.txt
- ref_texture_img.png
- source_mesh.obj
- source_caption.txt
- source_img.jpg
- meterial.mtl
- metrerial_0.png



