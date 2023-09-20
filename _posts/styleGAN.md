---
title: 'StyleGAN2'
categories: [Data Science, Deep Learning]
tags: [gan, cv]
math: 'True'
img_path: "/assets/img/posting/"
---

<div align=left>
  <img src="https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white">
  <img src="https://img.shields.io/badge/Jupyter%20Notebook-F37626?logo=jupyter&logoColor=white">
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?logo=pytorch&logoColor=white">
  <img src="https://img.shields.io/badge/macOS-000000?logo=apple&logoColor=white">
</div>


---

## Style Transfer
**Style Transfer** involves maintaining the **content** of an image while seamlessly rendering the **style** of another image to create a transformation. 

![Style Transfer 1](2023-02-01-styleGAN_styletransfer-1.png)

**Content Image** is the image that contains the actual content to be transformed. The structure and form of this image are reflected in the final result.\
**Style Image** carries the style that you want to apply. Its visual features such as colors, textures, and patterns are reflected in the final result.

<br>

### Texture Representation
**Texture** is the attribute that uniformly presents itself accross all spaces. In other words, it is the statistics without **spatial information**.


![Texture](2023-02-01-styleGAN_check_texture.png){: width="40%" height="40%"}{: .center}

CNN has **Convolution Layer**, which performs convolutional operations using filters(kernels) on small regions of an image. This process detects and extracts various features(i.g. textures) within the image.\
The feature map of the CNN serves as the content representation. Two images which make similar feature maps have similar contents. Because *'They have same interim findings'* means that *'They have same input images'*.

<br>

![Style Transfer 1](2023-02-01-styleGAN_styletransfer-2.png)

+ The style image $\bar{\alpha}$ is passed through the network and its style representation $A^l$ on all layers included are computed and stored.
+ The content image $\bar{p}$ is passed through the network and the content resresentation $P^l$ in one layer is stored.
+ A random white noise image $\bar{x}$ is passed through the network and its style features $G^l$ and content features $F^l$ are computed.

$\rightarrow$ The total loss $L_{total}$ is a linear combination between the content and the style loss.

![Style Transfer 1](2023-02-01-styleGAN_styletransfer-3.png){: width="80%" height="80%"}

This figure illustrate the appearance with changing $\alpha / \beta$ ratio.\
Increasing $\alpha$ reveals more of the source image, increasing $\beta$ reduces the source image.

<br>

### Discusion
However, it is not clear what exactly defines the **content** and **style** of an image.\
Style might be the brush strokes in a painting, the color map, cetain dominant forms and shapes, but also the composition of a scene and the choice of the subject of the image and probably it is a mixture of all of them and many more.


## StyleGAN


---

# References
* LA Gatys, AS Ecker, M Bethge. (2016). [Image Style Transfer using Convolutional Neural Networks.](https://openaccess.thecvf.com/content_cvpr_2016/html/Gatys_Image_Style_Transfer_CVPR_2016_paper.html)
* T Karras, S Laine, T Aila. (2019). [A Style-Based Generator Architecture for Generative Adversarial Networks.](https://arxiv.org/abs/1812.04948)