# Rapid Gram-stain Image Analysis
Rapid Gram-stain image analysis by means of convolutional neural networks implemented on notebooks using Keras/Tensorflow

Table of contents:
- Rapid Gram-stain Image Analysis
	- Installation
	- CNN models
	- Data
	- Benchmark on mobile devices
	- Bibtex
	- Changelog

## Installation
```
docker pull tensorflow/tensorflow:2.6.0-gpu-jupyter
```
## Overview

## CNN models
Three pretrained models were utilized in order to avoid model selection bias. They are namely Inception [21], ResNet [22], and MobileNet [23]. Inception was chosen because it is the most prevalent model utilized in the medical domain according to Morid et al. [24] and Kim et al [19]. Furthermore, ResNet is the most widely used backbone model for other tasks such as object detection and segmentation [25]. Finally, MobileNet was selected because it was explicitly designed to be deployed to resource constrained-devices [23]. 

## Data
The approval of the Data Protection office is currently in the works. As soon as we get approval, we will add data to the GitHub repository and update the readme file accordingly. Meantime, we will provide the link to the DIBaS database which is a publicly accessible gram stain image dataset: https://github.com/gallardorafael/DIBaS-Dataset. 

## Benchmark on mobile devices
- Reference: https://www.androidrecovery.com/blog/install-use-adb-windows.html
- Install Android Debug Bridge (adb) on Windows
- Activate the developer mode on the mobile device
- Press Shift key and right click within the extracted folder, then choose Open PowerShell window 
```
Example:
C:\Users\[USER_FOLDER]\AppData\Local\Android\Sdk\platform-tools
```
- Install the benchmark app on the phone
```
Example:
cd .\install\
adb install -r -d -g android_arm_benchmark_model_plus_flex.apk
OR
adb install -r -d -g android_aarch64_benchmark_model_plus_flex.apk
```
- Push the model file to the phone 
```
Example:
cd ..\model\
adb push mobilenet_BS64_FT100.tflite /data/local/tmp 
```
- Test the model on the phone
```
Example:
adb shell am start -S -n org.tensorflow.lite.benchmark/.BenchmarkModelActivity --es args "'--num_threads=1 --use_gpu=false --graph=/data/local/tmp/mobilenet_BS64_FT100.tflite'"
```

## Bibtex
19.	Kim HE, Cosa-Linan A, Santhanam N, Jannesari M, Maros ME, Ganslandt T. Transfer learning for medical image classification: a literature review. BMC Medical Imaging 2022 Apr 13;22(1):69. [doi: 10.1186/s12880-022-00793-7]21.	Szegedy C, Liu W, Jia Y, Sermanet P, Reed S, Anguelov D, Erhan D, Vanhoucke V, Rabinovich A. Going deeper with convolutions. Proceedings of the IEEE conference on computer vision and pattern recognition 2015. p. 1–9.
22.	He K, Zhang X, Ren S, Sun J. Deep residual learning for image recognition. Proceedings of the IEEE conference on computer vision and pattern recognition 2016. p. 770–778.
23.	Howard AG, Zhu M, Chen B, Kalenichenko D, Wang W, Weyand T, Andreetto M, Adam H. Mobilenets: Efficient convolutional neural networks for mobile vision applications. arXiv preprint arXiv:170404861 2017;
24.	Morid MA, Borjali A, Del Fiol G. A scoping review of transfer learning research on medical image analysis using ImageNet. Computers in biology and medicine. 2021 Jan 1;128:104115.
25.	Lee Y, Hwang JW, Lee S, Bae Y, Park J. An energy and GPU-computation efficient backbone network for real-time object detection. InProceedings of the IEEE/CVF conference on computer vision and pattern recognition workshops 2019 (pp. 0-0).

