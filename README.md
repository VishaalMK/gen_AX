_ImageNet Dataset_
![imagenet](/images/entry.jpg)

### Motivation
The goal of this project is to explore the effectiveness of state-of-the-art generative models towards purifying adversarial examples on ImageNet. The intuition behind this is simple, if generative models do what they do best, i.e, to estimate the underlying density of the training data (implicitly or explicitly), then they could be used to transform the adversarial examples closer to the true manifold of the training images. The reason this should work is that, by definition adversarial examples are imperceptible to the clean examples but end up being misclassified. Likewise, well-trained generative models _should_ be able to make out enough from the input adversarial image so as to transform it to the true distribution that it was trained on. 

### Related Work
This approach would also go hand in hand with an existing hypothesis that states that adversarial examples lie on a low probability region of the training distribution and that they could be made less effective (in terms of leading to misclassification) if they are somehow transformed into the high probability regions. And explicit generative models could come in handy here as they can be used to explicitly approximate and maximise the underlying probability density (as shown by [PixelDefend](https://openreview.net/forum?id=rJUYGxbCW)). 
There have been some previous work along these lines apart from PixelDefend, namely [MagNet](https://arxiv.org/abs/1705.09064) - which makes use of autoencoders to detect and transform the adversarial images; [DefenseGAN](https://openreview.net/forum?id=BkJ3ibb0-) which iterates in the latent space to generate an identical image to the input adversarial image by minimizing the reconstruction loss.

### Experiments
In this work, we test three models
1. **Plug & Play Generative Networks: Conditional Iterative Generation of Images in Latent Space [(PPGN)](https://github.com/Evolving-AI-Lab/ppgn)**
    * For details pertaining to purifying AXs using PPGN, refer to the documentations [here](https://docs.google.com/document/d/11ceQtk9_52y6i3Hi3Pgb5djb0HNkDcPqxAufEJaSjcs/edit?usp=sharing), [here](https://docs.google.com/document/d/1LKLhJO9SzFvyy6_JMul5Vo2H9aTo-kr1FI4HE_76cv8/edit?usp=sharing) and [here](https://docs.google.com/document/d/1w7gBrtSQPDwLNupIyODFFIy3kwLqtx9wFj_YZNrTvZs/edit?usp=sharing).

    *AXs generated on ImageNet Validation set*
    ![adv](/images/adv.jpg)

    *Transformed by PPGN*
    ![pure](/images/purified.jpg)

1. **[Deep Image Prior](![imagenet](/images/entry.jpg))**

    _Working of Deep Image Prior_

    ![dip](/images/twet.jpeg)

1. **[Context Encoders](https://github.com/pathak22/context-encoder): Feature Learning by Inpainting**

    _AXs inpainted by Context Encoder trained on ImageNet_
    ![ce](/images/val_21.png)

1. **Resizing/Scaling Images - used as a baseline**
    * For details refer to the documentation [here](https://docs.google.com/document/d/1uR7mQtjJ6HjHU815Zfct-zimCgUNDsRX1sd8aw3bAMo/edit?usp=sharing).
    * Detailed insights regarding this experiment can be found [here](https://docs.google.com/document/d/1_q5NrV1YWJUcWQ9lCkIyOZuKq0Pm4rM2khy2k_nESDQ/edit?usp=sharing).

### Results
* 100 randomly selected images from the ImageNet test set were used for these experiments
* Inception-v1 was the classifier used

**Image Type** | **Accuracy(Top-1)** | **Accuracy(Top-3)**
------------ | ------------- | -------------
Normal | 63% | 79% 
Adversarial FGSM eps=16 | 12%| 25%
PPGN purified | 18% | 33%
Deep Image Prior purified | 30% | 58%
CE-center region | 14% | 25%
Rescaling 224->112->224(2x) | 36% | 54%






