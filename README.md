# CNN-simplicity
Design several convolutional neural networks implementing concepts in "Strive for Simplicity" and Model Ensembling.

## Simple 5-layer CNN

We implement a simple 5-layer CNN with maxpooling in Deep-CNN-V2.ipynb, and achieved up to 87% validation accuracy, 83% test accuracy and ensemble test accuracy of 87%. 

We widen the CNN in Deep-CNN-V1.ipynb. This increases test accuracy to 85.2% and ensemble test accuracy to 88%.


## Strive for Simplicity
 
We improve on this by following the general direction proposed by "Strive for Simplicity":  
https://arxiv.org/abs/1412.6806  

The general idea is that an all-CNN network can equal or outperform current state-of-the-art CNNs by:

* Replace maxpool layer with a convolutional layer of stride=2  
* The linear layer can be replaced with a "network-in-network" structure  

In real practice, we discover that replacing maxpooling with a convolutional layer (stride=2) achieve the same 2:1 downsampling while increasing the learning ability of the CNN. However, we also discover that average pooling degrades CNN performance in general. In addition, we discover that simple data augmentation such as Horizontal Flip can improve accuracy without lengthening training time. 

In Simplicity.ipynb, we replace the 1st of the 2 maxpool layer with convolutional layer (stride=2), and achieve 89.6% validation accuracy, 87.2% single model test accuracy and 90.2% ensemble test accuracy. 

In Simplicity-V2, we replace the remaining maxpool layer with with convolutional layer (stride=2). While validation accuracy increases to 91.1%, there is no further improvement to single model (87.3) or ensemble test accuracy (90.3%). 

## Ensemble Averaging

In the course of implementing the CNNs above, we discover that Ensemble Averaging can improve test accuracy by 4-5% for all these models.

In LeGrandMix.ipynb, we conduct an experiment to see how the improvements from ensemble averaging is dependent on:

* Ensemble size  
* Model inclusion criteria  

Using the 100 model parameter files of over 100 permutations for the simple 5-layer CNN, we randomly create 200 random ensembles of size 2, 4, 6, 8 , 10 and 12 and then compute the means and std of test accuracies they achieve.

As predicted, as ensemble size increases, test accuracy increases and standard deviation decreases. For Model 1, an ensemble of size 10 increases test accuracy form 0.8223 to 0.8656 (an increase of 4.3%). This is in line with our results in DeepCNN-V2. Furthermore, the standard deviation decreases 3X from 0.0059 to 0.0021. 

*** So in a nutshell, ensemble of 8-12 is almost always a good thing!!! ***

 
