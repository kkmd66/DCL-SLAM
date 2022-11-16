# DCL-SLAM

 - The source code will be opened soon!

A ROS package of DCL-SLAM: Distributed Collaborative LiDAR SLAM Framework for a Robotic Swarm. 

https://user-images.githubusercontent.com/41199568/197691132-3850b5ff-8c6b-4bce-befa-a33f72487d2d.mp4

The HD video of the demonstration of DCL-SLAM is avaliable at [BiliBili](https://www.bilibili.com/video/BV12G4y187mw/?spm_id_from=333.337.search-card.all.click).

## Prerequisites
  - [Ubuntu ROS](http://wiki.ros.org/ROS/Installation) (Robot Operating System on Ubuntu 18.04 or 20.04)
  - Python (For wstool and catkin tool)
  - CMake (Compilation Configuration Tool)
  - [Boost](http://www.boost.org/) (portable C++ source libraries)
  - [PCL](https://pointclouds.org/downloads/linux.html) (Default Point Cloud Library on Ubuntu work normally)
  - [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page) (Default Eigen library on Ubuntu work normally)
  ```
  sudo apt-get install cmake libboost-all-dev python-wstool python-catkin-tools
  ```
  - [GTSAM](https://github.com/borglab/gtsam/releases) (Georgia Tech Smoothing and Mapping library)
  - [livox_ros_driver](https://github.com/Livox-SDK/livox_ros_driver) (The driver for Livox LiDAR)
  These prerequisites will be installed during the compilation.

## Compilation
  Set up the workspace configuration:
  ```
  mkdir -p ~/cslam_ws/src
  cd ~/cslam_ws
  catkin init
  catkin config --merge-devel
  catkin config --cmake-args -DCMAKE_BUILD_TYPE=Release
  ```
  
  Then use wstool for fetching catkin dependencies:
  ```
  cd src
  git clone https://github.com/PengYu-Team/DCL-SLAM.git
  git clone https://github.com/PengYu-Team/DCL-LIO-SAM.git
  git clone https://github.com/PengYu-Team/DCL-FAST-LIO.git
  wstool init
  wstool merge DCL-SLAM/dependencies.rosinstall
  wstool update
  ```

  Build DCL-SLAM
  ```
  catkin build dcl_lio_sam
  catkin build dcl_fast_lio
  ```
  
## Run with Dataset
  - [S3E dataset](https://github.com/PengYu-Team/S3E). The datasets are configured to run with default parameter.
  ```
  roslaunch dcl_slam run.launch
  rosbag play *your-bag-path*.bag
  ```
  
  - Other dataset. Please follow [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM) and [FAST-LIO2](https://github.com/hku-mars/FAST_LIO) to set your own config file for the dataset in "config/*your-config-file*.yaml", and change the path in "launch/single_ugv.launch".

## Citation
The paper is avaliable at [site](https://arxiv.org/pdf/2210.11978.pdf), and please cite:

```
@article{DBLP:journals/corr/abs-2210-11978,
  author    = {Shipeng Zhong and
               Yuhua Qi and
               Zhiqiang Chen and
               Jin Wu and
               Hongbo Chen and
               Ming Liu},
  title     = {{DCL-SLAM:} {A} Distributed Collaborative LiDAR {SLAM} Framework for
               a Robotic Swarm},
  journal   = {CoRR},
  volume    = {abs/2210.11978},
  year      = {2022},
  url       = {https://doi.org/10.48550/arXiv.2210.11978},
  doi       = {10.48550/arXiv.2210.11978},
  eprinttype = {arXiv},
  eprint    = {2210.11978},
  timestamp = {Tue, 25 Oct 2022 14:25:08 +0200},
  biburl    = {https://dblp.org/rec/journals/corr/abs-2210-11978.bib},
  bibsource = {dblp computer science bibliography, https://dblp.org}
}
```

## Acknowledgement

  - DCL-LIO-SAM adopt [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM) as front end (Shan, Tixiao and Englot, Brendan and Meyers, Drew and Wang, Wei and Ratti, Carlo and Rus Daniela. LIO-SAM: Tightly-coupled Lidar Inertial Odometry via Smoothing and Mapping).

  - DCL-FAST-LIO adopt [FAST-LIO2](https://github.com/hku-mars/FAST_LIO) as front end (Xu, Wei, Yixi Cai, Dongjiao He, Jiarong Lin, and Fu Zhang. Fast-lio2: Fast direct lidar-inertial odometry).

  - DCL-SLAM is based on a two-stage distributed Gauss-Seidel approach (Siddharth Choudhary and Luca Carlone and Carlos Nieto and John Rogers and Henrik I. Christensen and Frank Dellaert. Distributed Trajectory Estimation with Privacy and Communication Constraints: a Two-Stage Distributed Gauss-Seidel Approach).

  - DCL-SLAM is based on outlier rejection of [DOOR-SLAM](https://github.com/lajoiepy/robust_distributed_mapper) (Lajoie, Pierre-Yves and Ramtoula, Benjamin and Chang, Yun and Carlone, Luca and Beltrame, Giovanni. DOOR-SLAM: Distributed, Online, and Outlier Resilient SLAM for Robotic Teams).
