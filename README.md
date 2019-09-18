# GeometricPritraining

This is the project page of the paper **"Geometric Pretraining for Monocular Depth Estimation''**.

GeometricPritraining is a pretrain task designed specifically for depth estimation. The pretrain task requires only **uncalibrated** images from existing datasets or the internet. After the pretraining stage, the backbone network can be transferred to depth estimation tasks. Using unlimited images from the internet, we demonstrate that the geometric-pretrained networks perform better than ImageNet-pretrained networks by a large margin. **At the time of the submission, the proposed geometric pretrained networks achieve the new state-of-the-art performance using only existing training methods.**

This project page contains:

* the implementation of the pretrain task,

* the scripts to extract training images from internet videos.

* the geometric pretrained networks and the corresponding transferred depth estimation networks.

All components will be open source once the paper is accepted.

## The proposed method

The proposed method uses a conditional encoder-decoder network to reconstruct the optical flow between two images. With a narrow bottleneck, the encoder network is forced to learn motion-invariant structure information. After the pretraining, the encoder can be transferred to depth estimation using existing methods (e.g. [Monodepth2](https://github.com/nianticlabs/monodepth2)). The system is illustrated in the following figure.

<p align="center">
<img src="fig/system.png" alt="input_output" width = "750" height = "200">
</p>

After the pretrain, the transferred network show better accuracy, generalization ability, and few-shot learning.

* The KITTI-trained network tested on KITTI dataset:

GeoPt is geometric pretrained backbone. Click each photo for full resolution.

<table align='center'>
<tr>
<td><img src='fig/0.png' width='320' height='300'/></td>
<td><img src='fig/1.png' width='320' height='300'/></td>
<td><img src='fig/2.png' width='320' height='300'/></td>
</tr>
</table>

* The KITTI-trained network tested on CityScapes:

<table align='center'>
<tr>
<td><img src='fig/cs0.png' width='320' height='280'/></td>
<td><img src='fig/cs1.png' width='320' height='280'/></td>
<td><img src='fig/cs2.png' width='320' height='280'/></td>
</tr>
</table>

* The KITTI-trained network tested on YouTube videos: [Video1](https://youtu.be/seSjNF6EMyE) and [Video2](https://youtu.be/52kT5FDyk1M).
<p align="center">
<a href="https://youtu.be/wlobHEpPXDU" target="_blank"><img src="https://img.youtube.com/vi/wlobHEpPXDU/hqdefault.jpg" 
alt="video" width="432" height="316" border="10" /></a>
<a href="https://youtu.be/5AKuyMUk4w8" target="_blank"><img src="https://img.youtube.com/vi/5AKuyMUk4w8/hqdefault.jpg" 
alt="video" width="432" height="316" border="10" /></a>
</p>

## The proposed dataset DrivingVideos

There are countless of images on the internet. In this project, we build the pretrain dataset, DrivingVideos, using videos from the internet. Due to the current size of the pretrain dataset, we mixed the pretraining dataset using KITTI, CityScapes, and DrivingVideos. We are still enlarging the dataset. In the future, we will use only DrivingVideos for the pretraining as experiments show that this leads to the best transferred performance. For more details please check the paper.

A tipical sample from DrivingVideos is a 3-frame sequential image with no calibration informatiom:

<p align="center">
<img src="fig/drivevideo.jpg" alt="input_output" width = "1066" height = "160">
</p>

## The pretrained networks and transferred depth networks

Here, we provide the pretrained networks and transferred depth networks ([Monodepth2](https://github.com/nianticlabs/monodepth2) is used for the transferring). For details, please check the paper.

Backbone Networks:

| Model | Layer Num. | Resolution | KITTI | CityScapes | DrivingVideos_small | DrivingVideos_big | Link |
| ----- | ---------- | ---------- | ----- | ---------- | ------------------- | ----------------- | ---- |
| kcd   | 18         | 640x192    | Yes   | Yes        | Yes                 | No                | ---- |
| kc    | 18         | 640x192    | Yes   | Yes        | No                  | No                | ---- |
| d     | 18         | 640x192    | No    | No         | No                  | Yes               | ---- |
| kcd_hd| 50         | 1024x320   | Yes   | Yes        | Yes                 | No                | ---- |

Transferred Networks (evaluation using the code from Monodepth2):

| Backbone| Training Mode | Abs Rel | Sq Rel | RMSE | RMSE log | delta < 1.25 | Link |
| ------- | ------------- | ------- | ------ | ---- | -------- | ------------ | ---- |
| kcd_hd  | MS (1024x320) | 0.093   | 0.704  | 4.367| 0.183    | 0.896        | ---- |
| kcd_hd  | MS (640x192)  | 0.099   | 0.757  | 4.547| 0.187    | 0.888        | ---- |
| kcd     | MS (640x192)  | 0.105   | 0.804  | 4.693| 0.193    | 0.874        | ---- |
|   d     | M  (640x192)  | 0.112   | 0.820  | 4.707| 0.189    | 0.879        | ---- |
|   d     | S  (640x192)  | 0.105   | 0.816  | 4.820| 0.204    | 0.869        | ---- |
