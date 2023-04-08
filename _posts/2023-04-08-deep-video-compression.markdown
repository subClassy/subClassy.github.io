---
layout: post
title:  "Deep Video Compression"
date:   2023-04-08 14:53:00 -0700
categories: compression 
permalink: compression
description: Deep Video Compression
image:
  path: ../assets/images/compression/jj-ying-WmnsGyaFnCQ-unsplash.jpg
  height: 1200
  width: 630
comments: true
---

I few weeks ago, I wrote a blog post on 
[H.265 vs AV1: The Battle for Efficient Video Compression!](https://subclassy.github.io/compression).
Here I talked about the differences between H.265 and AV1 video compression 
standards and some experiments I did to compare them. In this post, I will
introduce the use of deep generative models for video compression and review 
some recent papers that apply this technique to various applications. Video 
compression is a fundamental problem in computer vision and multimedia, as it 
aims to reduce the storage and transmission costs of visual data while 
preserving its quality and information content. Traditional video compression 
methods rely on hand-crafted transforms, quantization schemes, and entropy 
coding algorithms that are designed based on human perception and signal 
processing principles. However, these methods have limitations in handling 
complex and diverse visual data, especially at low bitrates.

<img class="chatgpt-meme-drake" align="right" src="../assets/images/deep-video-compression/gptvsai.png" alt="chatgpt-meme" width="300"/>

Generative AI models have taken the world by storm in the recent history with
GPT based models, LLMs etc. However, generative models, such as variational 
autoencoders (VAEs) and generative adversarial networks (GANs), offer more than
just allowing you to talk to ChatGPT when you are alone!!


These models offer a new paradigm for video compression, as they can learn 
data-driven representations that capture the underlying structure and 
distribution of the visual data. Moreover, they can leverage powerful neural 
networks to perform nonlinear transforms, quantization, and entropy coding in 
an end-to-end manner. The main idea of deep generative models for video 
compression is to encode the input video into a compact latent representation 
that can be decoded by a generative model to reconstruct the original or a 
high-quality approximation of it. The latent representation can be further 
discretized and entropy coded to produce a compressed bitstream that can be 
transmitted or stored.

#### Research Papers

<subheading><h5>
<a href="https://openaccess.thecvf.com/content_CVPR_2019/papers/Lu_DVC_An_End-To-End_Deep_Video_Compression_Framework_CVPR_2019_paper.pdf">[1]</a>
<mark>DVC: An End-to-end Deep Video Compression Framework</mark>
</h5></subheading>

This paper by Lu et al., is the first paper to propose an end-to-end video 
compression deep model that jointly optimizes all the components for video 
compression. Simply put, they take the traditional video compression pipeline 
and replace each component with a neural network.

Specifically, learning-based optical flow estimation is utilized to obtain 
motion information and reconstruct current frames. Then two auto-encoder style 
neural networks are employed to compress the corresponding motion and residual 
information. 

The model consists of several key components: motion estimation and compression,
motion compensation, transform, quantization and inverse transform, entropy 
coding, and frame reconstruction. To make it simple to understand, I have taken
frames from the paper and annotated the image with the corresponding component.

| ![lu_2019](../assets/images/deep-video-compression/lu_2019.png "Figure A.1") | 
|:--:| 
| *Figure A.1 [1]* |

1. <strong>Motion estimation and Compression</strong> - a CNN model is used to 
estimate optical flow, which is considered as motion information. An motion 
vector encoder-decoder network is proposed to compress and decode optical flow 
values. 
2. <strong>Motion compensation</strong> - this network is designed to obtain the
predicted frame based on optical flow. 
3. <strong>Residual Encoding</strong> - The residual information between the 
original frame and predicted frame is encoded by a residual encoder network. A 
highly non-linear neural network is used to transform residuals to corresponding
latent representation. 
4. <strong>Quantization</strong> - The latent representations are required to be
quantized before entropy coding. 
5. <strong>Bit Rate Estimation Net</strong> - To estimate bit rates of generated
latent representations, CNNs are used to obtain probability distribution of each 
symbol.

Finally, frame reconstruction is performed by adding predicted frame and 
reconstructed residual.

<subheading><h5>
<a href="https://proceedings.neurips.cc/paper/2019/file/f1ea154c843f7cf3677db7ce922a2d17-Paper.pdf">[2]</a>
<mark>Deep Generative Video Compression</mark>
</h5></subheading>

#### References

[1] Lu, Guo, et al. "[Dvc: An end-to-end deep video compression framework.](https://openaccess.thecvf.com/content_CVPR_2019/papers/Lu_DVC_An_End-To-End_Deep_Video_Compression_Framework_CVPR_2019_paper.pdf)" 
Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition. 2019.

[2] Lombardo, Salvator, et al. "[Deep generative video compression.](https://proceedings.neurips.cc/paper/2019/file/f1ea154c843f7cf3677db7ce922a2d17-Paper.pdf)" Advances in Neural Information Processing Systems 32 (2019).