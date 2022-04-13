# Building-Damage-Detection-Using-Convolutional-Neural-Networks-

## Problem Statement 
After the damaged caused by hurricane lota, there are 61 fatalities and 41 people missing. For Relief Squads to reach them, it is important to quantify the buildings with damage, which is usually done by driving around and is time consuming. The task in hand is to propose a solution to identify damaged and not damaged buildings using there satellite images, a sample shown below:

Damaged: 

![image](https://user-images.githubusercontent.com/62461730/163123873-045d3aca-3e58-4973-b362-d122cfb7ab50.png)

Undamaged: 

![image](https://user-images.githubusercontent.com/62461730/163123664-904e5855-55ce-4103-8423-da896f5e63ae.png)

## Proposed Solution

1) Building a CNN from scratch and provide the classification.

2) Transfer Learning: Using a SOTA network and modifying it to provide the classification.

## Dataset 
1) The data set consists of satellite images of buildings and areas affected by lota hurricane. The clarity of the images is low. The data can be found <a href='https://www.kaggle.com/datasets/kmader/satellite-images-of-hurricane-damage' target='_blank'>here</a>

2) We Augmented the data using keras’s ImageDataGenerator adding rotation, zoom, height modifications etc to the data.

## Model Architechtures 
1) CNN From Scratch: Two CNN’s were build form scratch. The first one used the basic architecture of  5 convolution layers with kernel size of 5*5 and 3*3 and relu activation followed by 2 dense layers with 400 neurons each and relu activation. The output was a single neuron dense layer with sigmoid activation. Total number of parameters exceeding 4M. Dropout was the only regularization technique used in dense layers.The second CNN had the same structure as above but used a dilation rate of 2 in some of the convolution layers.

2) Transfer Learning: In our second approach we unleash the power of transfer learning using NASNet Mobile SOTA network. We froze 500 initial layers from training and train the rest with our modifications( GAP, Dense layers(2, with 1024 and 512 neurons respectively, and relu activation)) and a final  dense layer for binary output using sigmoid activation.

## Results

![image](https://user-images.githubusercontent.com/62461730/163125856-704d68b1-f208-4d63-9390-18580a41588d.png)

![image](https://user-images.githubusercontent.com/62461730/163125987-621e48f4-61ed-4dba-a3bf-4c86a737d878.png)

Transfer learning as expected outperformed the diluted CNN. The diluted CNN reached a respective accuracy and transfer learning model was next to perfect.

### Inferences 












