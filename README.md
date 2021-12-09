# ResNet50 Yeast classification

## Language used
python and Pytorch

This is a ResNet50 Model that is tailored for my specific yeast data.
Note the images imported are found in the UCSF severs. The data is NOT publicly available yet and therefore the link to access the data has been removed. 
Images used for training are single cell yeast cells that have been tracked overtime
Source images are resized to 40x40, cells are segmented using my previous image segmentation pipeline. 
eight phenotypes can be identified: Nuclear, aggregate, cytoplasm, triple, BinaryAggregate, Fragmented, circular, and Senescent
Senescent phenotype is also for dead cells
Aggregate phenotype includes the nuclear.


For training the model different parameters were used. In the end I settled with a specific set of augmentations, mini-batches, and utilizing a pretrained ResNet50 model. The pretrained ResNet50 model was trained on the 1 million ImageNET dataset. After experimenting I took the mean of the first convolutional layer as we are only inputing one image channel and the original pretrained model has three. I froze all the layers except for the first convolutional layer and the linear layer. 
Augmentations were based on previous analysis where I found them to help improve the model and prevent memorization! 

The standared practice of taking 10-20% of the total images was forsaken. Rather, using several imaging experiments, I hand curated a validation dataset. I picked difficult images with ~110-140 images for each category. If the standard practice of taking 10-20% of the data is used an inaccurate measure of ~95% accuracy is reached but the model does not reflect the actual ability for it to properly predict a phenotype when given new data. I have found the testing and training curves to be unreliable as in the past I had gotten excellent curves but terrible results. Thus, a cross-validation experiment is relied on to determine whether the retrained ResNet50 model is reliable. In the future I need to change the code to stop augmenting my cross-validation dataset when testing my model. This will smoothe the curves a bit.

I have also played with other portions including mini-batches, loss-functions, optimizers, MixUp, and CutMix. I have kept the parameters that I believe to help the model train. MixUp and CutMix did not help my model learn. 


The code reflects my parameters and written code to analyze my specific dataset. Links to where certain pieces of the codes can be found in the header of each cellblock.
