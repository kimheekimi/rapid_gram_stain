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
Codes can be seemlessly excuted in the docker container below.
Please pull the image of tensorflow/tensorflow:2.6.0-gpu-jupyter and run a container from the image.
```
docker pull tensorflow/tensorflow:2.6.0-gpu-jupyter
```
## Overview
Despite the emergence of mobile health and the success of deep learning (DL), deploying production-ready DL models to resource-limited devices remains challenging. Especially, during inference time, the speed of DL models becomes relevant. We aimed to accelerate inference time for Gram-stained analysis, which is a tedious and manual task involving microorganisms detection on whole slide images. Three DL models were optimized in three steps: transfer learning, pruning and quantization and then evaluated on two Android smartphones. Most convolutional layers (≥80%) had to be retrained for adaptation to the Gram-stained classification task. The combination of pruning and quantization demonstrated its utility to reduce the model size and inference time without compromising model quality. Pruning mainly contributed to model size reduction by 15x, while quantization reduced inference time by 3x and decreased model size by 4x. The combination of two reduced the baseline model by an overall factor of 46x. Optimized models were smaller than 6 MB and were able to process one image in <0.6 seconds on Galaxy S10. Our findings demonstrate that methods for model compression are highly relevant for the successful deployment of DL solutions to resource-limited devices.

## CNN models
Three pretrained models were utilized in order to avoid model selection bias. They are namely Inception, ResNet, and MobileNet. Inception was chosen because it is the most prevalent model utilized in the medical domain. ResNet is the most widely used backbone model for other tasks such as object detection and segmentation. Finally, MobileNet was selected because it was explicitly designed to be deployed to resource constrained-devices. 

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
Kim HE, Maros ME, Siegel F, Ganslandt T. Rapid Convolutional Neural Networks for Gram-Stained Image Classification at Inference Time on Mobile Devices: Empirical Study from Transfer Learning to Optimization. Biomedicines. 2022; 10(11):2808. https://doi.org/10.3390/biomedicines10112808
