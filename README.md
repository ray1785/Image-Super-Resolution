Image Super Resolution with CNN and Autoencoder. 

The dataset we used for training is COCO 2017 validation as our training dataset. 
Image Super Resolution with CNN and Autoencoder. 
It contains 5000 images and currently we only use 500 of them.  
We split the data into training set and test set with 80% /20% ratio.  

We further preprocessed our data with the following steps:
- We resized all the images to 300*300 resolution. These resized images are our expected outputs.
- We normalized the images (divided by 255)
- We shrink the image size to 150*150 then expand it back to 300 *300 to get low resolution images
- We blurred some images using Gaussian Blur
- We added 4 kinds of noises including Gaussian, salt and pepper, poisson, speckle some images. These distorted images are our Input
</BR>
Here’s our model architecture: </BR>

Model: "model"
__________________________________________________________________________________________________  
Layer (type)                    Output Shape         Param #     Connected to                       
==================================================================================================  
input_1 (InputLayer)            [(None, 300, 300, 3) 0                                            
__________________________________________________________________________________________________  
conv2d (Conv2D)                 (None, 300, 300, 64) 1792        input_1[0][0]                      
__________________________________________________________________________________________________  
conv2d_1 (Conv2D)               (None, 300, 300, 64) 36928       conv2d[0][0]                       
__________________________________________________________________________________________________  
max_pooling2d (MaxPooling2D)    (None, 150, 150, 64) 0           conv2d_1[0][0]                     
__________________________________________________________________________________________________  
conv2d_2 (Conv2D)               (None, 150, 150, 128 73856       max_pooling2d[0][0]                
__________________________________________________________________________________________________  
conv2d_3 (Conv2D)               (None, 150, 150, 128 147584      conv2d_2[0][0]                     
__________________________________________________________________________________________________  
max_pooling2d_1 (MaxPooling2D)  (None, 75, 75, 128)  0           conv2d_3[0][0]                     
__________________________________________________________________________________________________  
conv2d_4 (Conv2D)               (None, 75, 75, 256)  295168      max_pooling2d_1[0][0]              
__________________________________________________________________________________________________  
up_sampling2d (UpSampling2D)    (None, 150, 150, 256 0           conv2d_4[0][0]                     
__________________________________________________________________________________________________  
conv2d_5 (Conv2D)               (None, 150, 150, 128 295040      up_sampling2d[0][0]                
__________________________________________________________________________________________________  
conv2d_6 (Conv2D)               (None, 150, 150, 128 147584      conv2d_5[0][0]                     
__________________________________________________________________________________________________  
add (Add)                       (None, 150, 150, 128 0           conv2d_3[0][0]                     
                                                                 conv2d_6[0][0]                     
__________________________________________________________________________________________________  
up_sampling2d_1 (UpSampling2D)  (None, 300, 300, 128 0           add[0][0]                          
__________________________________________________________________________________________________  
conv2d_7 (Conv2D)               (None, 300, 300, 64) 73792       up_sampling2d_1[0][0]              
__________________________________________________________________________________________________  
conv2d_8 (Conv2D)               (None, 300, 300, 64) 36928       conv2d_7[0][0]                     
__________________________________________________________________________________________________  
add_1 (Add)                     (None, 300, 300, 64) 0           conv2d_1[0][0]                     
                                                                 conv2d_8[0][0]                     
__________________________________________________________________________________________________  
conv2d_9 (Conv2D)               (None, 300, 300, 3)  1731        add_1[0][0]                        
==================================================================================================  
Total params: 1,110,403.   
Trainable params: 1,110,403. 
Non-trainable params: 0. 
