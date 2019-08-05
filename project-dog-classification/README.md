[//]: # (Image References)

[image1]: ./images/sample_dog_output.png "Sample Output"
[image2]: ./images/vgg16_model.png "VGG-16 Model Layers"
[image3]: ./images/vgg16_model_draw.png "VGG16 Model Figure"


## Project Overview

In this project, you will learn how to build a pipeline that can be used within a web or mobile app to process real-world, user-supplied images.  Given an image of a dog, your algorithm will identify an estimate of the canine’s breed.  If supplied an image of a human, the code will identify the resembling dog breed.  

![Sample Output][image1]

Along with exploring state-of-the-art CNN models for classification and localization, you will make important design decisions about the user experience for your app.  Our goal is that by completing this lab, you understand the challenges involved in piecing together a series of models designed to perform various tasks in a data processing pipeline.  Each model has its strengths and weaknesses, and engineering a real-world application often involves solving many problems without a perfect answer.  Your imperfect solution will nonetheless create a fun user experience!

## Results
I trained a CNN from randomly initialized weights. Training this model from scratch was a highly iterative process. I started with just 5 convolution layers, 5 max pooling layers, and 3 dense layers with dropout at 0.25. It learned extremely slowly with loss decreasing by the thousandths and tens of thousandths, no matter what learning rate I chose or how many convolution layers I added. This led me to do some reading and I found the paper [Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift](https://arxiv.org/pdf/1502.03167.pdf) by Sergey Ioffe and Christian Szegedy. They found that by normalizing the output of convolutional layers they were able to stabilize gradient flow through the network thereby accelerating a networks's learning. 

Using this information, my next network consisted of 8 convolutional layers, each followed by batch normalization, ReLU, and 5 max pooling layers after certain convolution layers, and 3 fully connected layers. Dropout was initially set to p=0 and learning rate was set to 0.25, both the low dropout and high LR were allowed by the use of batch normalization. Compared to the previous networks, this networks's loss decreased by the tenths after each minibatch. As training progressed and the rate of validation loss decrease began to plateau, I lowered the LR by half. Furthermore, as training loss approached validation loss, I also slowly increased dropout until p=0.4. This protocol was followed for 42 epoch with the lowest validation loss recorded at epoch 40. This model reached 27% test accuracy. I suspect better accuracy could be achieved by conducting more experiments to find a good initial learning rate, intermittently increasing LR to find better minimums, adding convolutional layers, and simply letting the model train for more than 42 epochs.

