Here is the revised README content with the models that use ultralytics removed:

# YOLO Series TensorRT (Python/C++) 🚀

This repository provides support for various YOLO versions with TensorRT, enabling efficient inference on NVIDIA GPUs.

## Supported YOLO Versions
- [YOLOv10](https://github.com/THU-MIG/yolov10)
- [YOLOv9](https://github.com/WongKinYiu/yolov9)
- [YOLOv7](https://github.com/WongKinYiu/yolov7)
- [YOLOv6](https://github.com/meituan/YOLOv6)
- [YOLOX](https://github.com/Megvii-BaseDetection/YOLOX)
- [YOLOv3](https://github.com/ultralytics/yolov3)

## Recent Updates
- **2024-06-16**: Added support for YOLOv9 and YOLOv10. Updated TensorRT to version 10.0.
- **2023-08-15**: Added support for CUDA Python.
- **2023-05-12**: General updates.
- **2023-01-07**: Added support for YOLOv8.
- **2022-11-29**: Bug fixes (thanks to [JiaPai12138](https://github.com/JiaPai12138)).
- **2022-08-13**: Repository renamed and new version released. Added C++ support for end-to-end.
- **2022-08-11**: Added NMS plugin support with the `--end2end` flag in `export.py`.
- **2022-07-08**: Added support for YOLOv7.
- **2022-07-03**: Added support for TRT INT8 post-training quantization.

## Preparing the TensorRT Environment
### Install via Python
```shell
pip install tensorrt
pip install cuda-python
```

### Install via C++ 🛠️
You can use [Docker](https://github.com/NVIDIA/TensorRT/blob/main/docker/ubuntu-20.04.Dockerfile) to set up the C++ environment.

## Usage Instructions

### YOLOv10
#### Generate TRT File
```shell
python export.py -o yolov10n.onnx -e yolov10.trt --end2end --v10 -p fp32
```
#### Inference
```shell
python trt.py -e yolov10.trt -i src/1.jpg -o yolov10-1.jpg --end2end
```

### YOLOv9
#### Generate TRT File
```shell
python export.py -o yolov9-c.onnx -e yolov9.trt --end2end --v8 -p fp32
```
#### Inference
```shell
python trt.py -e yolov9.trt -i src/1.jpg -o yolov9-1.jpg --end2end
```

## Python Demos 📢
<details><summary><b>Expand</b></summary>

### YOLOv5
#### Clone Repository and Download Weights
```shell
git clone https://github.com/ultralytics/yolov5.git
wget https://github.com/ultralytics/yolov5/releases/download/v6.1/yolov5n.pt
```
#### Export ONNX
```shell
python yolov5/export.py --weights yolov5n.pt --include onnx --simplify --inplace
```
#### Include NMS Plugin
```shell
python export.py -o yolov5n.onnx -e yolov5n.trt --end2end
python trt.py -e yolov5n.trt -i src/1.jpg -o yolov5n-1.jpg --end2end
```
#### Exclude NMS Plugin
```shell
python export.py -o yolov5n.onnx -e yolov5n.trt
python trt.py -e yolov5n.trt -i src/1.jpg -o yolov5n-1.jpg
```

### YOLOX
#### Clone Repository and Download Weights
```shell
git clone https://github.com/Megvii-BaseDetection/YOLOX.git
wget https://github.com/Megvii-BaseDetection/YOLOX/releases/download/0.1.1rc0/yolox_s.pth
cd YOLOX && pip3 install -v -e . --user
```
#### Export ONNX
```shell
cd YOLOX
python tools/export_onnx.py --output-name ../yolox_s.onnx -n yolox-s -c ../yolox_s.pth --decode_in_inference
```
#### Include NMS Plugin
```shell
python export.py -o yolox_s.onnx -e yolox_s.trt --end2end
python trt.py -e yolox_s.trt -i src/1.jpg -o yolox-1.jpg --end2end
```
#### Exclude NMS Plugin
```shell
python export.py -o yolox_s.onnx -e yolox_s.trt
python trt.py -e yolox_s.trt -i src/1.jpg -o yolox-1.jpg
```

### YOLOv6
#### Download Weights
```shell
wget https://github.com/meituan/YOLOv6/releases/download/0.1.0/yolov6s.onnx
```
#### Include NMS Plugin
```shell
python export.py -o yolov6s.onnx -e yolov6s.trt --end2end
python trt.py -e yolov6s.trt -i src/1.jpg -o yolov6s-1.jpg --end2end
```
#### Exclude NMS Plugin
```shell
python export.py -o yolov6s.onnx -e yolov6s.trt
python trt.py -e yolov6s.trt -i src/1.jpg -o yolov6s-1.jpg
```

### YOLOv7 🤓
#### Clone Repository and Download Weights
```shell
git clone https://github.com/WongKinYiu/yolov7.git
wget https://github.com/WongKinYiu/yolov7/releases/download/v0.1/yolov7-tiny.pt
pip install -r yolov7/requirements.txt
```
#### Export ONNX
```shell
python yolov7/export.py --weights yolov7-tiny.pt --grid --simplify
```
#### Include NMS Plugin
```shell
python export.py -o yolov7-tiny.onnx -e yolov7-tiny.trt --end2end
python trt.py -e yolov7-tiny.trt -i src/1.jpg -o yolov7-tiny-1.jpg --end2end
```
#### Exclude NMS Plugin
```shell
python export.py -o yolov7-tiny.onnx -e yolov7-tiny-norm.trt
python trt.py -e yolov7-tiny-norm.trt -i src/1.jpg -o yolov7-tiny-norm-1.jpg
```

</details>

## Additional Notes 📌
This project is based on [TensorRT-For-YOLO-Series](https://github.com/Linaom1214/TensorRT-For-YOLO-Series/tree/cuda-python). Future updates will include optimization functions to enhance accessibility and performance.

