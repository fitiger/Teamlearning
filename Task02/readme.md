# Task02 Data loading and augmentation

### Load Image
In PyTorch, it use Pillow or OpenCV to load image
```py
# Pillow
img = Image.open('file')
# PyTorch use PIL image as default.
# OpenCV
img = cv2.imread('file')
# By default, the channel is BRG, and can be convert to RGB by
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```
All these operations run on CPU; however, `tf.data.Dataset` can run on GPU or TPU; the drawback is `tf.image` only have limited API.

### Data augmentation

Data augmentation is a tecnique to genarate more data based on existing data. The main reason is that in the image task, we always don't have enough data for training and data augmentation merely hurts performance. 

The most popular methods for data augmentation including:
- Rotation (90 or 190 degree)
- Flipping (horizontal or vertical depends on specific situation)
- Random brightness
- Random crop

### DataLoder (similar with tf.data.Dataset)

[Official tutorial](https://pytorch.org/tutorials/beginner/data_loading_tutorial.html) for DataLoder.

```py
import os, sys, glob, shutil, json
import cv2

from PIL import Image
import numpy as np

import torch
from torch.utils.data.dataset import Dataset
import torchvision.transforms as transforms

class SVHNDataset(Dataset):
    def __init__(self, img_path, img_label, transform=None):
        self.img_path = img_path
        self.img_label = img_label 
        if transform is not None:
            self.transform = transform
        else:
            self.transform = None

    def __getitem__(self, index):
        img = Image.open(self.img_path[index]).convert('RGB')

        if self.transform is not None:
            img = self.transform(img)
        
        # 原始SVHN中类别10为数字0
        lbl = np.array(self.img_label[index], dtype=np.int)
        lbl = list(lbl)  + (5 - len(lbl)) * [10]
        
        return img, torch.from_numpy(np.array(lbl[:5]))

    def __len__(self):
        return len(self.img_path)

train_path = glob.glob('../input/train/*.png')
train_path.sort()
train_json = json.load(open('../input/train.json'))
train_label = [train_json[x]['label'] for x in train_json]

train_loader = torch.utils.data.DataLoader(
        SVHNDataset(train_path, train_label,
                   transforms.Compose([
                       transforms.Resize((64, 128)),
                       transforms.ColorJitter(0.3, 0.3, 0.2),
                       transforms.RandomRotation(5),
                       transforms.ToTensor(),
                       transforms.Normalize([0.485, 0.456, 0.406], [0.229, 0.224, 0.225])
                       # Using mean and std of Imagenet
            ])), 
    batch_size=10, # 每批样本个数
    shuffle=False, # 是否打乱顺序
    num_workers=10, # 读取的线程个数
)

for data in train_loader:
    break
```

[PyTorch Cheat Sheet](https://pytorch.org/tutorials/beginner/ptcheat.html) is an overview of essential PyTorch elements.
