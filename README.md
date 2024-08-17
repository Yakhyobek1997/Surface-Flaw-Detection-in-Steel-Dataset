Steel Surface Defect Detection Using PyTorch
This project aims to develop a PyTorch-based segmentation model to accurately identify defects on steel surfaces. The model employs a U-Net architecture with a ResNet encoder and is trained on the NEU Surface Defect Database provided by Northeastern University (NEU).

Dataset Overview
The NEU Surface Defect Database contains six types of common surface defects found on hot-rolled steel strips:

Rolled-in scale (RS)
Patches (Pa)
Crazing (Cr)
Pitted surface (PS)
Inclusion (In)
Scratches (Sc)
All images are grayscale and have a resolution of 200x200 pixels. The database consists of 1,800 images, with 300 samples per defect type. You can access the dataset here.

Below is an example image from the dataset:



Project Workflow
Data Preparation
Before training, the dataset was split into training and validation sets. We used the Create_Validation_Images.ipynb script to randomly select five images from each defect class for validation. These images, along with their corresponding annotations, were moved to the Validation_Images and Validation_Annotations folders, ensuring they were excluded from the training process.

Model Training
The model training was conducted using PyTorch, with CUDA support for accelerated computation. We experimented with various architectures, including:

U-Net with ResNet34 encoder
FPN (Feature Pyramid Network) with ResNet34 encoder
FPN with InceptionV4 encoder
FPN with Xception encoder
The training process involved the following steps:

Execute one of the Train_Segmentation_Model scripts to initiate the training.
The Trainer.py script is called to manage the training loop, while Data_Retriever_Seg.py handles data loading.
After each epoch, the model’s performance is evaluated using metrics like Dice Coefficient. If a better validation score is achieved, the model state is saved.
Inference
Inference was conducted using the Inference_Script.ipynb. This script loads a trained model and generates segmentation masks for the validation images. The predicted masks are compared with the ground truth annotations to assess performance.

Repository Structure
Key Folders
ANNOTATIONS: Contains XML files with defect location annotations.
IMAGES: Contains the original steel surface images used for training.
Validation_Annotations: Annotations for images reserved for final validation.
Validation_Images: Images reserved for final validation.
Models: Stores the trained model files (.pth format).
Utilities: Contains utility scripts for model training, evaluation, and inference.
Key Scripts
Meter.py: Contains logic for computing evaluation metrics (e.g., IOU, Dice Coefficient).
Trainer.py: Manages the model training process.
Data_Retriever_Seg.py: Handles data loading for training and testing.
Resnet_Unet.py: Defines the U-Net model architecture with a ResNet encoder.
Create_Validation_Images.ipynb: Script for separating images for validation.
Exploratory_Data_Analysis.ipynb: Provides initial data analysis.
Train_Segmentation_Model: Scripts for training different segmentation models.
Inference_Script.ipynb: Used for generating segmentation masks during inference.
