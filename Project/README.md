# StyleGAN encoder for image-to-image translation

This is the repository of the final project proposed for the course of *Vision and Perception*.

This work is intended to master skills in Deep Learning for Computer Vision and is centered on the idea of developing the generic **pixel2style2pixel(pSp)** framework presented in the paper [Richardson et al, **"Encoding in Style: a StyleGAN Encoder for Image-to-Image Translation,"** (IROS 2016)](https://arxiv.org/abs/2008.00951) and aplicable  on a large variety of **image-to-image translation** tasks. It is implemented in Tensorflow.

## The pSp Framework

Given an input image, **x**, the output of the model is defined as:

$$pSp(\mathbf{x}) := G(E(\mathbf{x}) + \mathbf{\bar{w}})$$

where $E(·)$ and $G(·)$ denote the novel pSp encoder with a FPN architecture that generates style vectors directly in extended latent space $\mathit{W}+$ and a pretrained StyleGAN generator, respectively.

The complete architecture is illustrated in image below.

## Authors
- Olga Sorokoletova - 1937430
- Amila Sikalo - 1938032
