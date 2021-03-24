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

