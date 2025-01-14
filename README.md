# Ultrasound_Nerve_Segmentation

## Introduction of ultrasound nerve dataset

## Getting the code
You can download all the files in this repository by cloning this repository:
```
https://github.com/Jia-Wei-Liao/Ultrasound_Nerve_Segmentation.git
```

## Repository structure
```
      .
      ├──checkpoint
      |   └──2021-12-31-02-33-20-best
      ├──dataset
      |   ├──train
      |   |   ├──X_X.tif
      |   |   └──X_X_mask.tif
      |   ├──test
      |   |   └──X.tif
      |   ├──train_masks.csv
      |   ├──Train_X.csv
      |   └──Valid_X.csv
      ├──src
      |   ├──configs.py
      |   ├──dataset.py
      |   ├──transforms.py
      |   ├──model.py
      |   ├──metric.py
      |   ├──logger.py      
      |   ├──trainer.py
      |   ├──RLE.py
      |   └──utils.py
      ├──train.py
      └──inference.py
```

## Requirements
```
tqdm
numpy
pandas
matplotlib
PIL
pillow
opencv-python
torch
torchvision
monai
segmentation_models_pytorch
```

## Dataset
You can download the dataset on the Google Drive:
<>

## Pre-trained weight
You can download the weight and checkpoint of our model and config on the Google Drive:
<https://drive.google.com/drive/folders/1FE5c0MQWQNB5wXRFlOryf95LSg7agkFf?usp=sharing>

## Training
To train the model, you can run this command:
```
python train.py \
-bs 8 \
-ep 100 \
--dataset 2 \
--model smp_unet \
--pretrain efficientnet-b1 \
--activation RELU \
--loss DFL \
--optim adamw \
--lr 5E-4 \
--weight_decay 1e-4 \
--scheduler cos \
--step_size 1 \
--gamma  0.95 \
--device cuda:0 \
--weight_num 10 \
--fliplr 0.5 \
--flipud 0.25 \
--bright 0.1 \
--noise 0.1
```

--dataset: 1, 2, 3, 4, 5
- model: monai_unet, smp_unet, smp_unetpp
- msih: 0, 1
- pretrain: resnet{34, 50}, resnext50_32x4d, efficientnet-b0, timm-resnest{14, 26, 50}d
- loss: DL, GDL, DCEL, DFL
- optim: sgd, adam, adamw
- scheduler: step, cos
- device: cpu or cuda:{0, 1, 2, 3}


## Inference
To inference the results, you can run this command:
```
python inference.py \
--adaptive <use adaptive ensemble>
--checkpoint <checkpoint's filename> \
--ensem_num <number of ensemble weight> \
```

## Reproducing submission
To reproduce our submission, please do the following steps:
1. [Getting the code](https://github.com/Jia-Wei-Liao/Ultrasound_Nerve_Segmentation/#Getting-the-code)
2. [Install the package](https://github.com/Jia-Wei-Liao/Ultrasound_Nerve_Segmentation/#requirements)
3. [Download the dataset](https://github.com/Jia-Wei-Liao/Ultrasound_Nerve_Segmentation/#dataset)
4. [Download the weight of model](https://github.com/Jia-Wei-Liao/Ultrasound_Nerve_Segmentation/#pre-trained-weight)
5. [Inference](https://github.com/Jia-Wei-Liao/Ultrasound_Nerve_Segmentation/#Inference)

## Experiments
| method       | backbone        | private score |
| ------------ | --------------- | ------------- |
| UNet         | ResNet50        | 0.69587       |
| UNet         | EﬀicientNet-b1  | 0.71954       |
| DeepLabv3+   | EﬀicientNet-b0  | 0.69328       |

## Citation
```
@misc{
    title = {nuclear_dataset_segmentation},
    author = {Jia-Wei Liao, Kuok-Tong Ng, Yi-Cheng Hung},
    url = {https://github.com/Jia-Wei-Liao/Ultrasound_Nerve_Segmentation},
    year = {2022}
}
```

## Reference
[1] https://github.com/qubvel/segmentation_models.pytorch  

[2] https://github.com/Project-MONAI/MONAI
