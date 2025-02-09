# RepVGG

***
> [RepVGG: Making VGG-style ConvNets Great Again](https://arxiv.org/pdf/2101.03697.pdf)

## Introduction

***
RepVGG, a vgg-style architecture that outperforms many complex models

Its main highlights are:

1) The model has a normal (a.k.a. feedforward) structure like vgg, without any other branches, each layer takes the
   output of its only previous layer as input, and feeds the output to its only next layer.

2) The body of the model uses only 3 × 3 conv and ReLU.

3) The specific architecture (including specific depth and layer width) is instantiated without automatic search, manual
   refinement, compound scaling, and other complicated designs.

## Benchmark

***

| Model           | Context   |  Top-1 (%)  | Top-5 (%)  |  Params (M)    | Train T. | Infer T. |  Download | Config | Log |
|-----------------|-----------|-------|-------|------------|-------|--------|---|--------|--------------|
| RepVGG_A0 | GPU | 71.98     | 90.36     |       |  |   | [model]() | [cfg]() | [log]() |
| RepVGG_A0 | D910x8-G | 71.87 | 90.43     |        |   |   | [model]() | [cfg]() | [log]() |

#### Notes

- All models are trained on ImageNet-1K training set and the top-1 accuracy is reported on the validatoin set.
- Context: GPU_TYPE x pieces - G/F, G - graph mode, F - pynative mode with ms function. 

## Examples

***

### Train

- The [yaml config files](../../configs) that yield competitive results on ImageNet for different models are listed in
  the `configs` folder. To trigger training using preset yaml config.

  ```shell
  comming soon
  ```

- Here is the example for finetuning a pretrained RepVGG_A0 on CIFAR10 dataset using Adam optimizer.

  ```shell
  python train.py --model=RepVGG_A0 --pretrained --opt=adam --lr=0.001 ataset=cifar10 --num_classes=10 --dataset_download
  ```

  Detailed adjustable parameters and their default value can be seen in [config.py](../../config.py)

### Eval

- To validate the model, you can use `validate.py`. Here is an example to verify the accuracy of pretrained weights.

  ```shell
  python validate.py --model=RepVGG_A0 --dataset=imagenet --val_split=val --pretrained
  ```

- To validate the model, you can use `validate.py`. Here is an example to verify the accuracy of your training.

  ```shell
  python validate.py --model=RepVGG_A0 --dataset=imagenet --val_split=val --ckpt_path='./ckpt/RepVGG_A0-best.ckpt' 
  ```
