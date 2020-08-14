# Yolov2 
This repository aims to learn and understand the YOLO algorithm. 
I am a beginner of deep learning, 
and I found the best way to learn a deep learning algorithm is to implement it from scratch.
So if you also feel this way, just follow this repo! 
The code in this projects is clear and easier to understand, 
and I also documented it as much as possible. 
## Demo
**Download the pretrained weights**

```
wget http://pjreddie.com/media/files/yolo-voc.weights
```
or
百度云：链接: https://pan.baidu.com/s/1IB9_ssrceKHsqbq7dvMMIw  密码: vvdd

**运行**    
You can run the demo with `cpu` mode

    python demo.py

Or with `gpu` mode

    python demo.py --cuda true
## 1.目录介绍
```text
|--checkpoints          checkpoints目录
|--config               配置目录
    |--config               配置解释
    |--config.py            配置文件
|--data                 数据集
|--dataset              读取数据集的库
    |--factory.py           工厂类
    |--imdb.py              imdb类
    |--pascal_voc.py        pascal类
    |--roidb.py             roidb类
    |--voc_eval.py          voc验证类
|--images               测试图片
|--models               模型库
    |--darknet.py           darknet
    |--loss.py              损失函数
    |--yolov2.py            yolov2
|--output               模型输出目录
|--util                 工具库
    |--augmentation.py      数据增强
    |--bbox.py              bbox
    |--network.py           network
    |-- visualize.py        visualize
|--requirements.txt     环境
|--demo.py              演示
|--test.py              验证
|--train.py             训练
|--yolo_eval.py         验证
```
## 2.环境准备
详细看requirements.txt文件。   
## 3.数据集准备  
#### **Download the training data.**    
```shell
wget http://host.robots.ox.ac.uk/pascal/VOC/voc2007/VOCtrainval_06-Nov-2007.tar
wget http://host.robots.ox.ac.uk/pascal/VOC/voc2007/VOCtest_06-Nov-2007.tar
wget http://host.robots.ox.ac.uk/pascal/VOC/voc2007/VOCdevkit_08-Jun-2007.tar

# download 2012 data
wget http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar
```
或者从百度云下载，   
链接: https://pan.baidu.com/s/1OkIP4SKXzrNtOCMsCtTBbA  密码: 2nko

#### **Extract the training data**    
all the data will be in one directory named VOCdevit. 
We use $VOCdevit to represent the data root path
```shell
tar xvf VOCtrainval_06-Nov-2007.tar
tar xvf VOCtest_06-Nov-2007.tar
tar xvf VOCdevkit_08-Jun-2007.tar

# 2012 data
tar xvf VOCtrainval_11-May-2012.tar
```
It should have this basic structure    
```
$VOCdevkit/                           # development kit
$VOCdevkit/VOCcode/                   # VOC utility code
$VOCdevkit/VOC2007                    # image sets, annotations, etc.
```
#### Create symlinks for the PASCAL VOC dataset
```shell
cd yolov2 # 也就是项目根目录
mkdir data
cd data
mkdir VOCdevkit2007
cd VOCdevkit2007
ln -s $VOCdevit/VOC2007 VOC2007

mkdir VOCdevkit2012
cd VOCdevkit2012
ln -s $VOCdevit/VOC2012 VOC2012
```
## 4.Train
#### Download pretrained network
```
cd yolov2
cd data
mkdir pretrained
cd pretrained
wget https://pjreddie.com/media/files/darknet19_448.weights
```
#### train
`python train.py --cuda true`

If you want use multiple GPUs to accelerate the training. you can use the command below.

`python train.py --cuda true --mGPUs true`
## 5.Predict

`python test.py --cuda true`

## 6.mAP

| | training set | test set | mAP@416 | mAP@544 |
| :--: | :--: | :--: | :--: | :--: |
|this repo|VOC2007+2012|VOC2007|72.7|74.6|
|original paper|VOC2007+2012|VOC2007|76.8|78.6|

Running time: ~19ms (52FPS) on GTX 1080

## 7.效果图

## 参考
[原项目地址](https://github.com/tztztztztz/yolov2.pytorch)