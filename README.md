# Research experiment logs

My work is now focusing on combining Semantic Information with Domain Generation, so I write my experiment log here. 

### 2021.12.24

Christmas Eve, chocolate drinks from zy, thx.

A bug was found in faster_rcnn.py, line 68.

Word vectors are generated from index of label words, not the word itself.

Code in test_net.py also made this mistake, fixed.

Bug fixed and retraining networks with 'true' semantic labels...

Result:

AP for aeroplane = 0.0000
AP for bicycle = 0.0002
AP for bird = 0.0000
AP for boat = 0.0000
AP for bottle = 0.0000
AP for bus = 0.0000
AP for car = 0.0000
AP for cat = 0.0007
AP for chair = 0.0000
AP for cow = 0.0000
AP for diningtable = 0.0000
AP for dog = 0.0303
AP for horse = 0.0000
AP for motorbike = 0.0002
AP for person = 0.0014
AP for pottedplant = 0.0000
AP for sheep = 0.0000
AP for sofa = 0.0001
AP for train = 0.0000
AP for tvmonitor = 0.0002
Mean AP = 0.0017

册那

More bugs fixed, a line of weight init code in faster-rnn.py was found and modified.

Deleted reduce dim layer from 4 to 1 directly, and add tanh after that layer.

Separated se and bl codes.

### 2021.12.23

BaseLine:

AP for aeroplane = 0.5207
AP for bicycle = 0.7173
AP for bird = 0.5351
AP for boat = 0.3100
AP for bottle = 0.3818
AP for bus = 0.6089
AP for car = 0.7326
AP for cat = 0.6954
AP for chair = 0.3188
AP for cow = 0.6530
AP for diningtable = 0.3305
AP for dog = 0.6586
AP for horse = 0.7295
AP for motorbike = 0.7040
AP for person = 0.6577
AP for pottedplant = 0.2458
AP for sheep = 0.6090
AP for sofa = 0.5029
AP for train = 0.5915
AP for tvmonitor = 0.5937
Mean AP = 0.5548

With Semantic Information:

AP for aeroplane = 0.0017
AP for bicycle = 0.1123
AP for bird = 0.0058
AP for boat = 0.0010
AP for bottle = 0.0021
AP for bus = 0.0033
AP for car = 0.0183
AP for cat = 0.0064
AP for chair = 0.0182
AP for cow = 0.0181
AP for diningtable = 0.0000
AP for dog = 0.0055
AP for horse = 0.0285
AP for motorbike = 0.0540
AP for person = 0.1619
AP for pottedplant = 0.0003
AP for sheep = 0.0065
AP for sofa = 0.0000
AP for train = 0.0003
AP for tvmonitor = 0.0000
Mean AP = 0.0222

Maybe some bugs in codes.

### 2021.12.22

Convert semantic vector to acc completely.

Before feeding data into mAP calculation part, calculate cosine similarity as acc directly.

### 2021.12.21

Modified RCNN-loss to L2, adding semantic embedding query module.

Mapping Feature Map to Semantic Vector, and calculate loss with true semantic vectors.

Using small dataset, 1000 images. Do remember delete pkl files in:

>'$Project_path/data/cache/'

>'$dataset_path/ImageSets/Main'

Next step is to overwrite mAP calculation in test phase.

### 2021.12.20

New Faster-R-CNN from: https://github.com/jwyang/faster-rcnn.pytorch/tree/pytorch-1.0

Modify the classification layer in 'faster-rcnn.pytorch-pytorch-1.0/lib/model/faster_rcnn/vgg16.py', line 50.

Batch size of classification layer could be changed in this project.

However, questions are listed as follow:

1. Is there any difference between projecting feature map into semantic space and mapping into same dimension?
2. Projection are same to referenced paper, mapping are to complicated?

~~Besides, RTX 2060 have not enough memory for Faster-R-CNN, servers are needed now.~~

Size of input image can be reshaped in file ‘faster-rcnn.pytorch-pytorch-1.0/lib/model/utils/config.py’, line 63.


### 2021.12.1

Raw word embedding tensor generation module finished.

Downloading 300d and 500d pretrained embeddings.

Interface on different dimision embeddings finished.

Modified three label words so it can be vectorized.

>diningtable -> table
>pottedplant -> plant
>tvmonitor -> monitor

~~Next step is debugging with voc2012 dataset. Remember that the classification layer was modified back to 512x1024, but input data are still 512x512.~~

Now the shape of each tensor have been reshaped properly. But the model is loading the whole weights.

Remove the weights, or modify the shape by adding several layers.


### 2021.11.29

Modify Faster-R-CNN module to add Self Attention module into classification subnet.

Downloading Word2Vec pretrained embeddings...English 100 dim.

### 2021.11.26

Self Attention module finished.

Do take care of the size of input and output.


### 2021.11.25

Giving up using Faster-R-CNN from torchvision because it is difficult to override Class.

Now using Faster-R-CNN from : https://github.com/lllsaaxx/Faster-RCNN

### 2021.11.22

Experiment environment are finished on PC, NOT server.

System: Ubuntu 20.04.3 LTS

NVIDIA-SMI 460.91.03    Driver Version: 460.91.03    CUDA Version: 11.2

Cuda compilation tools, release 11.2, V11.2.67   Build cuda_11.2.r11.2/compiler.29373293_0

Pytorch is instlled with this command:
>pip3 install torch==1.8.2+cu111 torchvision==0.9.2+cu111 torchaudio==0.8.2 -f https://download.pytorch.org/whl/lts/1.8/torch_lts.html

See this page in detail: https://medium.com/analytics-vidhya/install-cuda-11-2-cudnn-8-1-0-and-python-3-9-on-rtx3090-for-deep-learning-fcf96c95f7a1
