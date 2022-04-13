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
1) The data set consists of satellite images of buildings and areas affected by lota hurricane. The clarity of the images is low. The data can be found <a href='https://www.kaggle.com/datasets/kmader/satellite-images-of-hurricane-damage' target='_blank'>here.</a>

2) We Augmented the data using keras’s ImageDataGenerator adding rotation, zoom, height modifications etc to the data.

## Model Architechtures 
1) CNN From Scratch: Two CNN’s were build form scratch. The first one used the basic architecture of  5 convolution layers with kernel size of 5*5 and 3*3 and relu activation followed by 2 dense layers with 400 neurons each and relu activation. The output was a single neuron dense layer with sigmoid activation. Total number of parameters exceeding 4M. Dropout was the only regularization technique used in dense layers.The second CNN had the same structure as above but used a dilation rate of 2 in some of the convolution layers.

2) Transfer Learning: In our second approach we unleash the power of transfer learning using NASNet Mobile SOTA network. We froze 500 initial layers from training and train the rest with our modifications( GAP, Dense layers(2, with 1024 and 512 neurons respectively, and relu activation)) and a final  dense layer for binary output using sigmoid activation.

## Results

![image](https://user-images.githubusercontent.com/62461730/163125856-704d68b1-f208-4d63-9390-18580a41588d.png)

![image](https://user-images.githubusercontent.com/62461730/163125987-621e48f4-61ed-4dba-a3bf-4c86a737d878.png)

Transfer learning as expected outperformed the diluted CNN. The diluted CNN reached a respective accuracy and transfer learning model was next to perfect.

### Model Explanantions and Inferences
In this section we will look at how our model is predicting if a building is damaged or undamgaged using GradCam, Saliency Mapping, ScoreCam algorithm by visualizing their outputs.

#### Transfer Learning Model 

True Label: Damage
Predicted Label: Damage

![image](https://user-images.githubusercontent.com/62461730/163127907-2894f5e5-14b3-4bd7-8c52-cd199c077d39.png)

As can be noticed the above Saliency Map, the model looks at the buildings and the areas just around it to confirm if the building is damaged. GradCam and ScoreCam in this case points that the model looks that trees around it. 

True Label: No Damage 
Predicted Label: No Damage

![image](https://user-images.githubusercontent.com/62461730/163129086-35f1ddc6-ad1e-4c91-9c29-83ed68570e6f.png)

In this case you can notice all the three algorithms are pointing towards the same case, they suggest that the model is looking at the building and around it, which does logically make sense.

#### CNN with Dilation
In this case we use GradCam++ algorithm to visualize which part of the images of our model considers to be important for classifications.

True Label: Damage 
Predicted Label: Damage

Original Image:

![image](https://user-images.githubusercontent.com/62461730/163129650-6a35d189-3546-4844-bb85-8df016a35a52.png)

GradCam++ Inference:

![image](https://user-images.githubusercontent.com/62461730/163129787-6b67bf3e-2f0a-42f9-90ac-a642736b24fa.png)

The models looks on the building and just around it to check for damagae wich makes sense as it is detecting the building and by the help of its surrounding coming on a conclusion of damage.

True Label: No Damage
Predicted Label: No Damage

Original Image:

![image](https://user-images.githubusercontent.com/62461730/163130913-edb62c2a-3608-49db-a39c-fe0c03ad1622.png)

GradCam++ Inference:

![image](https://user-images.githubusercontent.com/62461730/163131110-8f60f8e1-dd18-40d3-aa50-1b4c04a1b5aa.png)

Similar to transfer learning our convolutional neural network built by using dilation in the later layers is also able locate buildings and look around it for any damage or flood.


### Additional Work

1) We took inferences by clipping a small square from the image and calculating the loss after clipping that sqaure. We repeated this process by clipping such squares from the image in the size of 32*32 and observed the change in the loss, corresponding to each clipping. We used the red channel of the image to create this heat map by providing increments w.r.t to the change in loss associated with the clipped portion in the red channel.

![image](https://user-images.githubusercontent.com/62461730/163132266-83ca2c52-49f6-4b3b-94bc-9fd0583f597b.png)

The above heatmaps shows that green area with some area around the houses is important for the model for classification. A hypothesis for such behaviour might be that the model is looking at the water level in and around these trees or some patterns around them which help it in recoginition.

2) To add to the challenge, we add  random noise to the images and retrain our transfer learning model to see how does it impacts our model accuracy and if our model is able to classify the buildings correctly. We also provide our model with some weapons to fight this battle with regularization. A sample from the newly formed noisy images is given below:

![image](https://user-images.githubusercontent.com/62461730/163132827-cd88475f-b446-4a8c-a9b8-9673cb1efd71.png)

We used the SOTA network used before to train on this noisy data and it was found that the model was robust to the added noise and only a small amount of accurcy as lost. The following image shows the result for the same:

![image](https://user-images.githubusercontent.com/62461730/163133205-fe8ca22b-3811-4ed5-ac0c-89c5acc94e10.png)

### Conclusion

Inferring from the above results, dilated-CNN works better and faster while providing us a larger receptive field to better understand the effect on a pixel by it’s surroundings. The ability to use transfer learning enabled us to solve the problem more accurately even after adding random noise to the images, the model didn’t loose much of its power of classifying the buildings. 




























