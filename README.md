# GeometricPritraining

This is the project page of the paper **"Geometric Pretraining for Monocular Depth Estimation''**.

GeometricPritraining is a pretrain task designed specifically for depth estimation. The pretrain task requires only **uncalibrated** images from existing datasets or the internet. After the pretraining stage, the backbone network can be transferred to depth estimation tasks. Using unlimitted images from the internet, we demonstrate that the geometric-pretrained networks perform better than ImageNet-pretrained networks by a large margin.

This project page contians:

* the implementation of the pretrain task,

* the scripts to extract training images from internet videos.

* the geometric pretrained netwroks and the corresponding transferred depth estimation networks.

All components will be open source once the paper is accepted.

## The proposed method

The proposed method uses a conditional encoder-decoder network to reconstruct the optical flow between two images. With a narror bottleneck, the encoder network are forced to learn motion-invariant structure information. After the pretraining, the encoder can be transferred to depth estimation. The system is illustrated in the following figure.

<p align="center">
<img src="fig/system.png" alt="input_output" width = "750" height = "200">
</p>

After the pretrain, the transferred network show better accuracy, generalization ability and few-shot learning.

We show the results fine tuned on KITTI dataset using the method proposed in [Monodepth2](https://github.com/nianticlabs/monodepth2).

The model on KITTI dataset (GeoPt is the model transferred from the proposed geometric pretrained backbone):

<table align='center'>
<tr>
<td><img src='fig/0.png' width='320' height='300'/></td>
<td><img src='fig/1.png' width='320' height='300'/></td>
<td><img src='fig/2.png' width='320' height='300'/></td>
</tr>
</table>

The model on CityScapes:

<table align='center'>
<tr>
<td><img src='fig/cs0.png' width='320' height='300'/></td>
<td><img src='fig/cs1.png' width='320' height='300'/></td>
<td><img src='fig/cs2.png' width='320' height='300'/></td>
</tr>
</table>

## The proposed dataset and tools

Training and evaluating neural networks require large-scale high-quality data. Different from the widely used dataset from [DeMoN](https://github.com/lmb-freiburg/demon), we propose to render the dataset in GTA5 as a supplementary. A similiar data, MVS-Synth, is proposed in [DeepMVS](https://phuang17.github.io/DeepMVS/index.html). Cameras in the MVS-Synth dataset usually moves in small translations. On the other hand, the proposed GTA-SfM dataset contains images with much larger view angle changes which is more close to structure-from-motion (SfM) applications. Below is the comparision of the proposed GTA-SfM (left) and MVS-Synth (right).

<p float="left" align="center">
  <img src="fig/gta.gif" title="GTA-SfM dataset" width = "320" height="256"/>
  <img src="fig/mvs.gif" title="MVS-Synth" width = "320" height="256" />
</p>