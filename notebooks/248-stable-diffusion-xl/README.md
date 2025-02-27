# Image generation with Stable Diffusion XL and Segmind Stable Diffusion 1B (SSD-1B) and OpenVINO

## Stable Diffusion XL

Stable Diffusion XL or SDXL is the latest image generation model that is tailored towards more photorealistic outputs with more detailed imagery and composition compared to previous Stable Diffusion models, including Stable Diffusion 2.1.

With Stable Diffusion XL you can now make more realistic images with improved face generation, produce legible text within images, and create more aesthetically pleasing art using shorter prompts.

![pipeline](https://huggingface.co/stabilityai/stable-diffusion-xl-base-1.0/resolve/main/pipeline.png)

[SDXL](https://arxiv.org/abs/2307.01952) consists of an [ensemble of experts](https://arxiv.org/abs/2211.01324) pipeline for latent diffusion: In the first step, the base model is used to generate (noisy) latents, which are then further processed with a refinement model specialized for the final denoising steps. Note that the base model can be used as a standalone module or in a two-stage pipeline as follows: First, the base model is used to generate latents of the desired output size. In the second step, we use a specialized high-resolution model and apply a technique called [SDEdit](https://arxiv.org/abs/2108.01073)( also known as "image to image") to the latents generated in the first step, using the same prompt. 

Compared to previous versions of Stable Diffusion, SDXL leverages a three times larger UNet backbone: The increase of model parameters is mainly due to more attention blocks and a larger cross-attention context as SDXL uses a second text encoder. The authors design multiple novel conditioning schemes and train SDXL on multiple aspect ratios and also introduce a refinement model that is used to improve the visual fidelity of samples generated by SDXL using a post-hoc image-to-image technique. The testing of SDXL shows drastically improved performance compared to the previous versions of Stable Diffusion and achieves results competitive with those of black-box state-of-the-art image generators.

In this tutorial, we consider how to run the SDXL model using OpenVINO.

We will use a pre-trained model from the [Hugging Face Diffusers](https://huggingface.co/docs/diffusers/index) library. To simplify the user experience, the [Hugging Face Optimum Intel](https://huggingface.co/docs/optimum/intel/index) library is used to convert the models to OpenVINO™ IR format.

The notebook provides a simple interface that allows communication with a model using text instruction. In this demonstration user can provide input instructions and the model generates an image.

The image below illustrates the provided user instruction and generated image example.

![text2img_example.png](https://user-images.githubusercontent.com/29454499/258652206-2673ab36-0da3-45e3-bb9e-8b5fe0ef7e41.png)

>**Note**: Some demonstrated models can require at least 64GB RAM for conversion and running.

### Notebook Contents

The tutorial consists of the following steps:

- Install prerequisites
- Download the Stable Diffusion XL Base model from a public source using the [OpenVINO integration with Hugging Face Optimum](https://huggingface.co/blog/openvino).
- Run Text2Image generation pipeline using Stable Diffusion XL base
- Run Image2Image generation pipeline using Stable Diffusion XL base
- Download and convert the Stable Diffusion XL Refiner model from a public source using the [OpenVINO integration with Hugging Face Optimum](https://huggingface.co/blog/openvino).
- Run 2-stages Stable Diffusion XL pipeline


## Segmind Stable Diffusion 1B (SSD-1B)

The [Segmind Stable Diffusion Model (SSD-1B)](https://github.com/segmind/SSD-1B?ref=blog.segmind.com) is a distilled 50% smaller version of the Stable Diffusion XL (SDXL), offering a 60% speedup while maintaining high-quality text-to-image generation capabilities. It has been trained on diverse datasets, including Grit and Midjourney scrape data, to enhance its ability to create a wide range of visual content based on textual prompts.

This model employs a knowledge distillation strategy, where it leverages the teachings of several expert models in succession, including SDXL, ZavyChromaXL, and JuggernautXL, to combine their strengths and produce impressive visual outputs.

### Image Comparison (SDXL-1.0 vs SSD-1B)
![image](https://user-images.githubusercontent.com/82945616/277419571-a5583e8a-6a05-4680-a540-f80502feed0b.png)
In this tutorial, we consider how to run the SSD-1B model using OpenVINO.
We will use a pre-trained model from the Hugging Face Diffusers library. To simplify the user experience, the Hugging Face Optimum Intel library is used to convert the models to OpenVINO™ IR format.

### Table of contents:
- [Install Prerequisites](#Install-prerequisites-Uparrow)
- [SSD-1B Base model](#SSD-1B-Base-model-Uparrow)
- [Select inference device SSD-1B Base model](#Select-inference-device-SSD-1B-Base-model-Uparrow)
- [Text2image Generation Interactive Demo](#Text2image-Generation-Interactive-Demo-Uparrow)

## Installation Instructions

This is a self-contained example that relies solely on its own code.</br>
We recommend  running the notebook in a virtual environment. You only need a Jupyter server to start.
For details, please refer to [Installation Guide](../../README.md).