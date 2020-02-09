# Google Audio Set classification with Keras and pytorch
Audio Set is a large scale weakly labelled dataset containing over 2 million 10-second audio clips with 527 classes published by Google in 2017. 

This codebase is an implementation of [1], where attention neural networks are proposed for Audio Set classification and achieves a mean average precision (mAP) of 0.360. 

## News!
In Dec. 2019, our latest research pretrained audio neural networks (PANNs) [2] have achieved an mAP of **0.439**. Code is available: https://github.com/qiuqiangkong/audioset_tagging_cnn

## Download dataset
We convert the tensorflow type data to numpy data and stored in hdf5 file. The size of the dataset is 2.3 G. The hdf5 data can be downloaded here https://drive.google.com/open?id=0B49XSFgf-0yVQk01eG92RHg4WTA

## Run
Users may optionaly choose Keras or pytorch as backend in runme.sh to run the code (default is pytorch). 

**./runme.sh**

## Results
Mean average precision (mAP) of different models. 
<pre>
------------------------------------------------------
Models                      mAP     AUC     d-prime
------------------------------------------------------
Google's baseline           0.314   0.959   2.452
average pooling             0.300   0.964   2.536
max pooling                 0.292   0.960   2.471
single_attention [1]        0.337   0.968   2.612
multi_attention [2]         <b>0.357</b>   <b>0.968</b>   <b>2.621</b>
feature_level_attention [3] <b>0.361</b>   <b>0.969</b>   <b>2.641</b>
------------------------------------------------------
</pre>

Blue bars show the number of audio clips of classes. Red stems show the mAP of classes. 

![alt text](https://github.com/qiuqiangkong/audioset_classification/blob/master/appendixes/data_distribution.png)

## Extract AudioSet embedding feature from a raw waveform. 
You may extract AudioSet embedding feature of your own audio file (Tensorflow required). 

First you need to download and put these two files in the root of this codebase: 

(1) **vggish_model.ckpt** from https://storage.googleapis.com/audioset/vggish_model.ckpt

(2) **vggish_pca_params.npz** from https://storage.googleapis.com/audioset/vggish_pca_params.npz

Second, run **CUDA_VISIBLE_DEVICES=0 python extract_audioset_embedding/extract_audioset_embedding.py**

More information can be found here: https://github.com/tensorflow/models/tree/master/research/audioset

## Citation
[1] Kong, Qiuqiang, Changsong Yu, Yong Xu, Turab Iqbal, Wenwu Wang, and Mark D. Plumbley. "Weakly Labelled AudioSet Tagging With Attention Neural Networks." IEEE/ACM Transactions on Audio, Speech, and Language Processing 27, no. 11 (2019): 1791-1802.

[2] Kong, Qiuqiang, Yin Cao, Turab Iqbal, Yuxuan Wang, Wenwu Wang, and Mark D. Plumbley. "PANNs: Large-Scale Pretrained Audio Neural Networks for Audio Pattern Recognition." arXiv preprint arXiv:1912.10211 (2019).

## External links
The original implmentation of multi-level attention neural network is created by Changsong Yu https://github.com/ChangsongYu/Eusipco2018_Google_AudioSet
