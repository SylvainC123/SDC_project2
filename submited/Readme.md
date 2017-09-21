

# Self-Driving Car Engineer Nanodegree
# Deep Learning
## Project: Build a Traffic Sign Recognition Program

##Note:
Thei is the revision 2 of the project. The modifications from the first submitted project are as follow:

 - Improvement of the graphic display for the sets analysis as suggested by the review.
 - Display of both the training results and validation result during the training phase to check possible over fitting
 - Modification of the samples images analysis and NN result performance (see paragraph "Model testing") in this document or jupyter notebook.


## Summary:
This repo contains my submission for the traffic sign recognition project for Udacity's Self-Driving Car Engineer Nanodegree program.

- `Traffic_Sign_Classifier v1.0.html` contains the executed code from image loading to training and testing the deep neural network
- `/tranined_weights` contains the saved weights for the final network
- `/traffic_sign_example_images` contains 6 sample colour images of signs used to challenge the trained network

## Network Performance:
The final network has training and validation accuracies of over ~95% and a testing accuracy of over 93%.

## Network Architecture:
My final architecture is similqar to the leNet-5 network, made of two convolution layers followed by two fully connected layers.

*General model structure*:

layer 1: 
    

 - convolution :
           - 5x5 filter, input depth of 1, output depth of 6
           - 32x32x1 => 28x28x6
 - Activation with Relu ,        max(0,x)         
 - Pooling 
                - 2x2 kernel with 2x2 stride
                - 28x28x6 => 14x14x6
     
layer 2:

 - convolution :
- 5x5 filter, input depth of 6, output depth of 16
- 14x14x16 => 10x10x16
 - Activation with Relu, max(0,x)
 - Pooling 
           - 2x2 kernel with 2x2 stride
           - 10x10x16 => 5x5x16

output is flatten into a vector

layer 3: 
   

 - vector passed through a fully connected layer:
          - input size 400
           - output size 120
 - Activation with Relu, max(0,x)

        
Layer 4:
    

 - vector passed through a fully connected layer
          - input size 120
           - output size 84
 - Activation with Relu, max(0,x)

            
Layer 5:

 - vector passed through the output network
           input size= 84
           output size = number of labels = 43

## Training Architecture
Weights used in the constitutional layers and the the fully connected layers were initialised using a truncated normal distribution with a standard deviation of 0.1. 
Bias weights were initialised to zeros.

Image classes were transformed into one-hot encoding.

The model was trained using batch sets of 100.

A reduced mean, cross entropy loss function was fed the logits from the last fully connected layer. 
This loss was then minimised using an AdamOptimizer to which a decaying learning rate was added. 
The initial learning rate was set to 0.001 and exponentially decayed per each training step.

No dropout regularisation was used in this model, it could be a way to further improve the model's performance.

## Model testing
### Images tested
The model is tested on some traffic signs images extracted from the web and which do not belong to the original pool of images.
The image used present a good contast, and are similar to the one present in the training set, nevertheless the pre processing (size reduction + contrast + normalisation and centering) of those images tends to erase some of their characteristic features.

### NN result

The prediction performances are poor, despite good results on the test set.
2 out of 6 signs were properly identified as first estimation i.e. 33% accuracy compared to the 96% achieved on the validation set and 93% on  the test set.

The generalisation from signs which bo not belong to the original data is poor
Here are some possible explanation:

 - It looks like the NN do not detect fine details, a way to improve the
   system may be to add a convolution layer
 - Some images have got different pannel shape than the one on the
   training set, this may explain some of the errors
 - Some if the test images are bigger than the one in the test set
 - Possible data oferfitting

    
A modification of the model architecture may be needed to make it much more robust, a way to do so may be by :

 - using some dropout regularisation during the training
 - add some convolution steps to increase the degree of freedom of the system and the features recognition capability
 - increase of the training set size with 'jittering' the training images
 - try to improve the images pre treatment