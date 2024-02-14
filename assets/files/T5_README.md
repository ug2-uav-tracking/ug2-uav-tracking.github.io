# UG<sup>2</sup>+ CHALLENGE: UAV Tracking and Position Estimation



## About the Challenge
The proliferation and capabilities of small commercial unmanned aerial vehicles (UAVs) have introduced multifaceted security challenges that extend beyond conventional concerns. These easily accessible drones, available as commercial off-the-shelf products, pose significant threats across various domains.

This UG2+ Challenge is designed with the objective of integrating features from diverse modalities to achieve 3D UAV position estimation and classify the type of the UAV at the same time. Specifically, we provide fisheye camera images, millimeter-wave radar data, and lidar data obtained from Livox Mid360 and Livox Avia,  with ground truth provided by a Leica Nova MS60 Multi-Station.

### Data Structure

The training and validation data is organized into sequences, with each sequence encompassing the ground truth information for the position, image, Livox 360, Livox Avia, and mmWave radar data of the UAV. The structure of the published data is illustrated below:

```bash
Data
└───train
│   ├──seq0001
│   │   ├───ground_truth             # the ground truth position captured by leica
│   │   │    └───ros_timestamp.npy   # named with the corresponding timestamp
│   │   ├───class                   # the type of the flying uav
│   │   │    └───ros_timestamp.npy  
│   │   └───Image                    # the image captured by two fisheye camera
│   │   │    └───ros_timestamp.png  
│   │   └───lidar_360                # the lidar data captured by livox_mid360
│   │   │    └───ros_timestamp.npy
│   │   └───livox_avia               # the lidar data captured by livox_avia
│   │   │    └───ros_timestamp.npy
│   │   └───radar_enhance_pcl        # the radar data captured by mmwave radar
│   │   │    └───ros_timestamp.npy
	... ...
│   ├──seq0102
│     ... ...
└───val
│   ├──seq0001            
│   │   └───Image                    
│   │   └───lidar_360                
│   │   └───livox_avia               
│   │   └───radar_enhance_pcl        
│   ... ...
│   ├──seq0016

```

### The Calibration of the Fisheye Cameras
We offer the calibrated intrinsic parameters of fisheye cameras utilizing the omni camera model and radtan distortion model. Additionally, we supply the rosbag for camera calibration. Participants can select their preferred method for distortion correction and determine whether to perform it or not.


### Result Submission
The model's final performance will be evaluated on a hold-out test set comprising the same drone types and sensor types as the provided training set. 

 Participants are required to utilize the provided test data to infer both the position and the type of the drone at the given timestamps and **fill a .CSV file following the format specified below**

<table>

| Sequence (str) | Timestamp (float) |    Position (numpy float array)    | Classification (int) |
| :------------: | :---------------: | :--------------------------------: | :------------------: |
|    seq0001     | 1706255054.386069 |  [5.256965,  17.467245, 8.917183]  |          0           |
|    seq0001     | 1706255054.889673 |  [10.00370,  14.732623, 9.084157]  |          0           |
|    seq0001     | 1706255056.040618 |  [8.424405,  9.417857, 16.333868]  |          0           |
|    seq0002     | 1706255085.334848 |  [18.859711,  7.702462, 8.372803]  |          0           |
|    seq0002     | 1706255085.697843 | [10.778981,  17.909661, 12.957281] |          1           |
|    seq0002     | 1706255086.735852 | [9.909711,  -0.858245, 10.837073]  |          1           |

The CSV file is then required to be named as "**mmaud_results.csv**"  during the validation and final testing phases. Finally, participants are required to submit a **zip file containing only the CSV file** to Codabench for evaluation.

### Evaluation Metrix
The ranking criteria of this challenge will be based on i) **Mean Square loss** with respect to the ground truth label of the testing set and ii) the **Classification Accuracy** of the UAVs of the testing set.

