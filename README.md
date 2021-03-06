# how-do-vit-work

## Overview

1.	MSAs (multi-head self-attention) have been successful in computer vision, and this paper analyzes how visual translators (and convolutional architectures in contrast) work from an optimization standpoint.
2.	Paper presents an empirical analysis of Vision Transformers in particular multi-head self-attention and Convolutional networks with a focus on optimization-related properties.
3.	MSAs improve not only accuracy but also generalization by flattening the loss landscapes. Such improvement is primarily attributable to their data specificity, not long-range dependency.
4.	On the other hand, Vision Transformer suffer from non-convex losses. Large datasets and loss landscape smoothing methods alleviate this problem.
5.	Convs exhibit opposite behaviors. For example, MSAs are low-pass filters, but Convs are high-pass filters. Therefore, MSAs and Convs are complementary.
6.	Multi-stage neural networks behave like a series connection of small individual models. In addition, MSAs at the end of a stage play a key role in prediction. Based on these insights, they propose AlterNet, a model in which Conv blocks at the end of a stage are replaced with MSA blocks.
7.	The new hybrid model that takes the best of Vision Transformation and Convolutional networks and demonstrates good empirical performance not only in large data datasets but also in small data datasets.

### Model Structure

![image](https://user-images.githubusercontent.com/69946337/161376973-e1303efe-4615-47ad-abd3-437b226cf3e9.png)

This model integrates multi-head attention and convolutional neural networks, and this model uses the method of replacing Convs at the end of a stage with MSAs in Resnet to get better result.

## Discussing Topic 1

In this model, we use both MSAs and traditional convolutional neural networks. What is the difference between MSAs and traditional  convolutional neural networks?

![image](https://user-images.githubusercontent.com/69946337/161379157-e2723dd3-bb5b-4a89-9d1a-968f4e563c70.png)

MSAs and Convs exhibit opposite behaviors. Therefore, MSAs and Convs are complementary. For example, MSAs are low-pass filters, but Convs are high-pass filters. Likewise, Convs are vulnerable to high-frequency noise but that MSAs are vulnerable to low-frequency noise: it suggests that MSAs are shape-biased, whereas Convs are texture-biased. In addition, Convs transform feature maps and MSAs aggregate transformed feature map predictions.

## Discussion Topic 2

What properties of MSAs Do we need to improve optimization?

MSAs improve not only accuracy but also generalization by flattening the loss landscapes. Such improvement is primarily attributable to their data specificity, NOT long-range dependency On the other hand, ViTs suffers from non-convex losses. Their weak inductive bias and long-range dependency produce negative Hessian eigenvalues in small dataset.


## Discussion Topic 3

The authors propose that they use MSAs at the end of each stage. How do we determine which convolutional layers we need to replace with MSA? Will different alternatives have an impact on the final result of the model?

![image](https://user-images.githubusercontent.com/69946337/161379249-d9456d89-2864-4b8b-90fd-389812479aca.png)

Usually MSA just complements Conv (not replaces Conv), and MSA closer to the end of a stage improves predictive performance based on experimental findings. 
But in fact, We still need to determine the position of MSAs according to different neural network models. For example, in the Resnet, adding MSAs harm the accuracy in the c1 stage, so we still need to perform fine-tuning.

## Critical Thinking 

1. In this article, the authors said that the new hybrid network Alter-Net achieves good performance on both large and small datasets, but in fact, they only tested the performance of the alternet on the CIFAR-100 dataset, which is only a small dataset. Although they provide a theoretical explanation for this conclusion, I think this conclusion still lack the support of experimental data.

2. In this article, the author just tried this method of using MSAs instead of convolutional neural network in ResNet, but some of their conclusions are based on all CNNs, so I think they may need more follow-up research.

## Resource Links

Namuk Park, Songkuk Kim. How do vision transformer work. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, 2022.

Aravind Srinivas, Tsung-Yi Lin, Niki Parmar, Jonathon Shlens, Pieter Abbeel, and Ashish Vaswani. Bottleneck transformers for visual recognition. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, 2021.

Christian Szegedy, Vincent Vanhoucke, Sergey Ioffe, Jon Shlens, and Zbigniew Wojna. Rethinking the inception architecture for computer vision. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, 2016.

Phil Wang. Implementation of vision transformer. https://github.com/lucidrains/ vit-pytorch, 2021.


## Code demonstration

Code repo: https://github.com/zhuhfcod/how-do-vit-work

Code reference repo: https://github.com/xxxnell/how-do-vits-work

## Video recording

Video link: https://github.com/zhuhfcod/how-do-vit-work/tree/main/video_recording

