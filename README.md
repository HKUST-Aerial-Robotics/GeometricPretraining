# GeometricPritraining

This is the project page of the paper **"Geometric Pretraining for Monocular Depth Estimation''**.

GeometricPritraining is a pretrain task designed specifically for depth estimation. The pretrain task requires only **uncalibrated** images from existing datasets or the internet. After the pretraining stage, the backbone network can be transferred to depth estimation tasks. Using unlimitted images from the internet, we demonstrate that the geometric-pretrained networks perform better than ImageNet-pretrained networks by a large margin. **At the time of the submission, the proposed geometric pretrained networks achieves the new state-of-the-art performance using only existing training methods.**

This project page contians:

* the implementation of the pretrain task,

* the scripts to extract training images from internet videos.

* the geometric pretrained netwroks and the corresponding transferred depth estimation networks.

All components will be open source once the paper is accepted.

## The proposed method

The proposed method uses a conditional encoder-decoder network to reconstruct the optical flow between two images. With a narror bottleneck, the encoder network are forced to learn motion-invariant structure information. After the pretraining, the encoder can be transferred to depth estimation using existing methods (e.g. [Monodepth2](https://github.com/nianticlabs/monodepth2)). The system is illustrated in the following figure.

<p align="center">
<img src="fig/system.png" alt="input_output" width = "750" height = "200">
</p>

After the pretrain, the transferred network show better accuracy, generalization ability and few-shot learning.

The KITTI-trained network tested on KITTI dataset:

GeoPt is geometric pretrained backbone and click each photo for full resolution.

<table align='center'>
<tr>
<td><img src='fig/0.png' width='320' height='300'/></td>
<td><img src='fig/1.png' width='320' height='300'/></td>
<td><img src='fig/2.png' width='320' height='300'/></td>
</tr>
</table>

The KITTI-trained network tested on CityScapes:

<table align='center'>
<tr>
<td><img src='fig/cs0.png' width='320' height='300'/></td>
<td><img src='fig/cs1.png' width='320' height='300'/></td>
<td><img src='fig/cs2.png' width='320' height='300'/></td>
</tr>
</table>

## The proposed dataset DrivingVideos

There are countless of images on the internet. In this project, we build the pretrain dataset, DrivingVideos, using videos from the internet. Due to the current size of the pretrain dataset, we mixed the pretraining dataset using KITTI, CityScapes and DrivingVideos. We are still enlarging the dataset. In the future, we will use only DrivingVideos for the pretraining as experiments show that this leads to the best transferred performance. For more details please check the paper.

## The pretrained networks and transferred depth networks

Here, we provide the pretrained networks and transferred depth networks ([Monodepth2](https://github.com/nianticlabs/monodepth2) is used for the transferring). For details, please check the paper.

Backbone Networks:

| Model | Architecture | Resolution | use KITTI | use CityScapes | use DrivingVideos_small | use DrivingVideos_big | Link |
| ----- | ------------ | ---------- | --------- | -------------- | ----------------------- | --------------------- | ---- |
| kcd   | ResNet 18    | 640x192    | Yes       | Yes            | Yes                     | No                    | ---- |
| kc    | ResNet 18    | 640x192    | Yes       | Yes            | No                      | No                    | ---- |
| d     | ResNet 18    | 640x192    | No        | No             | No                      | Yes                   | ---- |
| kcd_hd| ResNet 50    | 1024x320   | Yes       | Yes            | Yes                     | No                    | ---- |


Transferred Networks:

| Backbone Model | Resolution | Training Mode | Abs Rel | Sq Rel | RMSE | RMSE log | delta < 1.25 | delta < 1.25^2 | delta < 1.25^3 | Link |
| -------------- | ---------- | ------------- | ------- | ------ | ---- | -------- | ------------ | -------------- | -------------- | ---- |
| kcd_hd         | 1024x320   | MS            | 0.093   | 0.704  | 4.367| 0.183    | 0.896        | 0.964          | 0.982          | ---- |
| kcd_hd         | 640x320    | MS            | 0.099   | 0.757  | 4.547| 0.187    | 0.888        | 0.961          | 0.981          | ---- |
| kcd            | 640x320    | MS            | 0.105   | 0.804  | 4.693| 0.193    | 0.874        | 0.958          | 0.980          | ---- |
|   d            | 640x320    | M             | 0.112   | 0.820  | 4.707| 0.189    | 0.879        | 0.961          | 0.982          | ---- |
|   d            | 640x320    | S             | 0.105   | 0.816  | 4.820| 0.204    | 0.869        | 0.952          | 0.976          | ---- |
