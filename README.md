# Sea-Life_Detection_with_YOLOv8
## Overview
This project aims to detect various types of sea life including sharks, jellyfish, fish, stingrays, and penguins. The detection of sea life is of significant importance in various domains such as marine biology, environmental conservation, and underwater robotics. Accurate identification and tracking of sea life can lead to better understanding and protection of marine ecosystems.

## Dataset
The dataset used in this project contains labeled images of sea life, with the following categories: shark, jellyfish, fish, stingray, and penguin. The dataset is obtained from Roboflow, and can be accessed using the provided API key.

## Algorithm
The project employs the YOLOv8 algorithm for object detection. YOLO (You Only Look Once) is a real-time object detection system that is both fast and accurate. YOLOv8 is a state-of-the-art version of the YOLO algorithm that has been optimized for various applications.

## Instructions and Environment Setup
Make sure you have an NVIDIA GPU available by running !nvidia-smi.

Install the necessary dependencies by running:

!pip install ultralytics==8.0.20
!pip install roboflow

## Training the Model
Download the dataset from Roboflow:

from roboflow import Roboflow

rf = Roboflow(api_key="YOUR_API_KEY")

project = rf.workspace("YOUR_WORKSPACE").project("YOUR_PROJECT")

dataset = project.version(1).download("yolov8")

## Train the YOLOv8 model:

!yolo task=detect mode=train model=yolov8s.pt data={dataset.location}/data.yaml epochs=200 imgsz=800 plots=True

## Model Evaluation
Confusion Matrix:

Image(filename=f'{HOME}/runs/detect/train/confusion_matrix.png', width=600)
## Results:
Image(filename=f'{HOME}/runs/detect/train/results.png', width=600)

## Validation Batch Prediction:
Image(filename=f'{HOME}/runs/detect/train/val_batch0_pred.jpg', width=600)

## Model Deployment
The trained model can be deployed on Roboflow for real-world applications:

project.version(dataset.version).deploy(model_type="yolov8", model_path=f"{HOME}/runs/detect/train/")

## Inference on Images/Videos
Run inference on images:

!yolo task=detect mode=predict model={HOME}/runs/detect/train/weights/best.pt conf=0.25 source={dataset.location}/test/images save=True

## Run inference on a video:

!yolo task=detect mode=predict model={HOME}/runs/detect/train/weights/best.pt conf=0.25 source='/content/drive/MyDrive/Certificates/20220719_173513.mp4' save=True

## Conclusion
This project addresses the crucial task of sea life detection using the YOLOv8 algorithm. By accurately identifying various sea creatures, we contribute to the broader efforts in marine biology and environmental conservation. The trained model can be easily deployed for real-time applications, making it a valuable tool for researchers and professionals in the field.
