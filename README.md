<img src="http://imgur.com/1ZcRyrc.png" style="float: left; margin: 20px; height: 90px">

# Capstone: Designing a Basic Self Drive Vehicle

## Table of Contents
1) [Overview](#Overview) 
2) [Data Dictionary](<#Data Dictionary>)
3) [Requirements](#Requirements)
4) [Executive Summary](<#Executive Summary>)
    1) [Purpose](<#Purpose>)
    2) [Data Handling](<#Data Handling>)
    3) [Analysis](#Analysis)
    4) [Findings and Implications](<#Findings and Implications>)
    5) [Next Steps](#Next-Steps)

## Overview
Self-driving initiatives are transforming the transportation industry by developing autonomous vehicles that can navigate and make decisions without human intervention. These systems rely on a combination of sensors (like cameras, radar, and LiDAR) and advanced machine learning algorithms to interpret real-time data, understand the environment, and safely control vehicle movement. Image-based models are a critical component, leveraging deep learning techniques to process visual information, such as road signs, obstacles, and traffic patterns, enabling the vehicle to act accordingly. With ongoing advancements, these technologies are aiming to improve road safety, reduce traffic congestion, and make transportation more efficient and accessible.

A Convolution Neural Network was employed to analyze images taken from the [Udacity self drive car dataset](https://github.com/udacity/self-driving-car/tree/master/datasets/CH2) in order to determine outputs in different driving scenarios such as speed, steering wheel angle, and braking. This would allow for a base starting point for companies that aspire to build self drive cars to reduce training time and help with inital image recognition.

## Data Dictionary
The data was collected from the Udacity open source self driving car [github](https://github.com/udacity/self-driving-car).

Vehicle Wheel Speed Report Information

| Information | Data Type | Description | Notes |
|---|---|---|---|
|`front_left_wheel`|`float`|Front left wheel speed in km/h|Renamed from `front_left`|
|`front_right_wheel`|`float`|Front right wheel speed in km/h|Renamed from `front_right`|
|`rear_left_wheel`|`float`|Rear left wheel speed in km/h|Renamed from `rear_left`|
|`rear_right_wheel`|`float`|Rear right wheel speed in km/h|Renamed from `rear_right`|

Vehicle Gear Report Information

| Information | Data Type | Description | Notes |
|---|---|---|---|
|`gear_state`|`float`|The current gear state of the vehicle.|Renamed from `state.gear`|
|`gear_cmd`|`float`|The commanded gear state.|Renamed from `cmd.gear`|

Vehicle Braking Report Information

| Information | Data Type | Description | Notes |
|---|---|---|---|
|`brake_lights_input`|`int`|The raw signal from the brake light activation sensor.|Renamed from `boo_input`. Changed from a bool value.|
|`brake_lights_output`|`int`|The actual state of the brake light.|Renamed from `boo_output`. Changed from a bool value.|
|`brake_pedal_input`|`float`|The raw signal from the brake pedal sensor.|Renamed from `pedal_input`|
|`brake_pedal_output`|`float`|The actual brake pedal position being applied.|Renamed from `pedal_output`|
|`brake_enabled`|`int`|Indicates whether the braking system is enabled.|Renamed from `enabled`. Changed from a bool value.|
|`brake_pedal_cmd`|`float`|The commanded brake pedal position.|Renamed from `pedal_cmd`|
|`torque_input`|`float`|The torque requested by the driver through the brake pedal.||
|`torque_cmd`|`float`|The commanded brake torque.||
|`torque_output`|`float`|The actual brake torque being applied.||

Vehicle Braking Info Report Information

| Information | Data Type | Description | Notes |
|---|---|---|---|
|`Time`|`float`|Time point the data was collected|Rounded to the fourth decimal place, which loses some data but allows the images to be matched to the data.|
|`brake_torque_request`|`float`|Amount of braking force the car system intends to supply.|This may be dropped later|
|`brake_torque_actual`|`float`|The real braking force applied by the vehicle.||
|`wheel_torque_actual`|`float`|The rotational force at the wheels that results from various inputs, such as braking, acceleration, or other mechanical forces.||
|`accel_over_ground`|`float`|How fast the vehicle is changing its speed in the horizontal direction.||
|`hill_start_assist_system_status`|`int`|Status of the hill assist sytstem to prevent the car from rolling down hills.|Renamed from `hsa.status`.|
|`hill_start_assist_mode`|`int`| Indicates if the hill start assist is engaged or not.|Renamed from `hsa.mode`.|
|`parking_brake_enabled`|`int`|Status of the parking brake if it is engaged or not.|Renamed from `parking_brake.status`.|
|`stationary`|`int`|If the car is moving or not.|Changed from a bool value.|
|`abs_active`|`int`|If the advanced braking system is actively regulating braking pressure to prevent wheel lockup.|Changed from a bool value.|
|`abs_enabled`|`int`|If the advanced braking system is enabled.|Changed from a bool value.|
|`stab_active`|`int`|Indicating whether the Electronic Stability Control (ESC) system is actively intervening to stabilize the vehicle.|Changed from a bool value.|
|`stab_enabled`|`int`|Indicates whether the Electronic Stability Control (ESC) system is enabled.|Changed from a bool value.|
|`trac_active`|`int`|Indicating whether the Traction Control System (TCS) is actively intervening to manage wheel slip.|Changed from a bool value.|
|`trac_enabled`|`int`|Indicates whether the Traction Control System (TCS) is enabled.|Changed from a bool value.|

Vehicle Throttle Info Information

| Information | Data Type | Description | Notes |
|---|---|---|---|
|`throttle_enabled`|`int`|Indicates whether the throttle control system is enabled.|Renamed from `enabled`. Changed from a bool value.|
|`throttle_pedal_input`|`float`|The raw input from the accelerator pedal sensor.|Renamed from `pedal_input`|
|`throttle_pedal_cmd`|`float`|The throttle command requested by the driver or an automated system.|Renamed from `pedal_cmd`|
|`throttle_pedal_output`|`float`|The actual throttle output being sent to the engine or motor.|Renamed from `pedal_output`|


Vehicle Throttle Info Report Information

| Information | Data Type | Description | Notes |
|---|---|---|---|
|`Time`|`float`|Time point the data was collected|Rounded to the fourth decimal place, which loses some data but allows the images to be matched to the data.|
|`throttle_pc`|`float`|How much the accelerator pedal is being pressed in percent.||
|`throttle_rate`|`float`|The rate in precent that the throttle position is changing.||
|`engine_rpm`|`float`|The speed at which the engine's crankshaft is rotating.||

Vehicle Steering Report Information

| Information | Data Type | Description | Notes |
|---|---|---|---|
|`Time`|`float`|Time point the data was collected|Rounded to the fourth decimal place, which loses some data but allows the images to be matched to the data.|
|`steering_wheel_angle`|`float`|The angle at which steering wheel is turned.||
|`steering_wheel_torque`|`float`|The amount of force being applied to turn the steering wheel.||
|`speed`|`float`|The vechile's speed in meters per second.|This was manipulated to kilometers per hour.|
|`steering_enabled`|`int`|A binary indicator (1 or 0) showing whether the steering system is currently active.|Renamed from `enabled`. Changed from a bool value.|

Internal Measurement Unit (IMU) Information

| Information | Data Type | Description | Notes |
|---|---|---|---|
|`Time`|`float`|Time point the data was collected|Rounded to the fourth decimal place, which loses some data but allows the images to be matched to the data.|
|`orientation_x`|`float`|The vehicles position in the `x` direction in 3D space in quaternion.|Defines how the vehicle is oriented relative to a fixed coordinate frame.|
|`orientation_y`|`float`|The vehicles position in the `y` direction in 3D space in quaternion.|Defines how the vehicle is oriented relative to a fixed coordinate frame.|
|`orientation_z`|`float`|The vehicles position in the `z` direction in 3D space in quaternion.|Defines how the vehicle is oriented relative to a fixed coordinate frame.|
|`orientation_w`|`float`|The scalar part of the quaternion used to encode the vehicles rotation in 3D space||
|`orientation_covariance_0-8`|`float`|Form a 3x3 covariance matrix that describes the uncertainty in the orientation measurements.|Lower values indicate higher confidence.|
|`angular_velocity_x`|`float`|The angular velocity of the vehicle around the `x` axis measured in radians per second.|These values are all `0` because a car does not rotate unless there is a crash and it tumbles.|
|`angular_velocity_y`|`float`|The angular velocity of the vehicle around the `y` axis measured in radians per second.|These values are all `0` because a car does not rotate unless there is a crash and it tumbles.|
|`angular_velocity_z`|`float`|The angular velocity of the vehicle around the `z` axis measured in radians per second.|These values are all `0` because a car does not rotate unless there is a crash and it tumbles.|
|`angular_velocity_covariance_0-8`|`float`|Form a 3x3 covariance matrix that describes the uncertainty in the angular velocity measurements.|Lower values indicate higher confidence. All values are `-1.0` because the car never rolled.|
|`linear_acceleration_x`|`float`|Acceleration in the forward/backward direction.|Measured in meters per second.|
|`linear_acceleration_y`|`float`|Acceleration in the lateral (side-to-side) direction.|Measured in meters per second.|
|`linear_acceleration_z`|`float`|Acceleration in the vertical (up/down) direction, often affected by gravity.|Measured in meters per second.|
|`linear_acceleration_covariance_0-8`|`float`|Form a 3x3 covariance matrix that describes the uncertainty in the linear acceleration measurements.|Lower values indicate higher confidence.|

## Requirements

### Hardware
The Convolution Neural Network (CNN) model is extremely memory intesive due in part to the large amount of images being processed. It is recommended that to repeat this work the user has at minimum 85 GB of RAM. Variables were saved for training the model to speed up training different itterations of the model. These files took up about 57 GB of space in total while the data for all the trips was about 60 GB including the images in total. 
### Software
| Library | Module | Purpose |
| --- | --- | --- |
| `numpy` || Ease of basic aggregate operations on data.|
| `pandas` || Read our data into a DataFrame, clean it, engineer new features, and write it out to submission files.|
| `matplotlib` | `pyplot`| Basic plotting functionality.|
| `sklearn` | | |
|  | `model_selection`| `train_test_split` for splitnting the data to test models on unseen data.|
| `os` | | Access operating level commands within python.|
| `random` | | To generate random seeds for easier analysis of models.|
| `gc` |  | To recover RAM used to save variables. |
| `joblib` | | `load` to load in saved variables.|
| | | `dump` to save variables for later use.|
| `PIL` |  | `Image` Python Imaging Library to work with images.|
| `gc` | | To reclaim memory no longer in use by objects. |
| `tensorflow` | `keras.models` | `Sequential` allows for the building of nueral networks layer-by-layer in a sequential order. |
|  |  | `load_model` loads in saved models for inference or retraining.|
| | `keras.layers` | `Input` specifies the shape an data type of the input data.|
|  |  | `Conv2D` applies filters to input data to extract spatial features. |
|  |  | `MaxPooling2D` pooling layer to reduce the spatial dimension of the input. |
|  |  | `Flatten` takes multi-dimensional input into a 1D vector. |
|  | | `Dense` a fully connected layer in a nerual network where each neureon in the layer is connected to every neuron in the previous layer.|
|  |  | `Dropout` randomly sets a fraction of the neurons to zero during training to help prevent overfitting.|
|  |  | `BatchNormalization` stabilizes training and improves performance. |
|  | `keras.optimizers` | `Adam` gradient decent algothrim optimized for large datasets.|
|  | `keras.callbacks` | `EarlyStopping` stops the training process when a given metric is met to prevent overfitting and unnecessary training time.|
| `io` |  | For efficient data processing when reading in images.|
| `bagpy` |  | Used to read and extract information from bag files. |
|  | | `bagreader` opens ROS bag files.|
| `rosbag` |  | Replays the recorded messages in ROS bag files for analysis or conversion to other formats. |
| `tqdm` | | `tqdm` track code progress visually with a loading bar.|

## Executive Summary

### Purpose
To take in only image data and have the model predict the state of the car and any inputs from the driver. The model should also be able to understand spacing between cars and the lines on the road for companies to use this as a starting point to train their models. To do this a Convolution Neural Network was employed to analyze the image data. 

### Data Handling
There were few nulls within the data once it was read in from the ROS bag files. The nulls that were present were usually the entire column that could not be read in. The column that was not able to be read ion and contained all null values was the column labeled `frame_id` and was dropped from all used datasets. 

When read in the dataset contained 5 different rides each with 36 csvs that contained varying amounts of information. The rides themselves were of different lengths and thus contained varying amounts of image data, when merged together there were about 33,000 images. The infromation used to train the models were in the imu-data, vehicle-brake_info_report, vehicle-steering_report, vehicle-throttle_info_report, vehicle-throttle_report, vehicle-gear_report, vehicle-brake_report, and vehicle-wheel_speed_report csvs.

Each dataset contained many features that were not used in the models. The features that were used are outlined above. The `Time` column was dropped from all models once the image data was associated with the corresponding information and all the datasets were merged in chronological order (trips were in time order and inputs for the trips were in time order).

Some feature names were changed so that there would be no conflicts when merging, since the names were the same in some csvs, and for clarity in the predictions analysis. These changes are documented above in the data dictionary. Some values were changed to integars from boolian values and those changes are also documented in the data dictionary above. Once the images were attachted appropriately to each dataset the csvs were outer merged and any resulting null values were dropped. These null values corresponded to information that contained no images or in some cases only a single image. Those that contained single images were the minority with the majority being inputs that contained no images. This resulted in a single csv with 74 different features, about 33,000 rows and 3 features that just contained the image paths for the different cameras. 

### Analysis
Initially the model was intended to be able to drive the car. This idea was set to the side due to the amount of computing power need to run the model and the amount of time needed to run the model being large constraints. Instead a Convolutional Neural Network (CNN) was designed to predict driving outputs based on the image presented. This reulted in a model with an MAE of about 30 and an MSE of about 36000. Showcasing that the model is able to fairly accurately predict desired driving outputs from just image data.

### Findings and Implications
Through looking at the predicted outputs for random images I found that the model is able to accurately predict what a driver would do in the situation in the image but the reactions are over pronounced. When the model sees brake lights for example it has correctly determined that cars are stopping but the model brakes too hard for what you would expect from a normal driver. The model also seems to overcompensate with trees or obsticles it sees on the sides of roads as it begins to brake based on the outputs. Spatial data would most likely help correct this issue.

### Next Steps
Future work would consist of setting up a virtual environment to test if the model is able to drive the car and take inputs from the camera on the car. Other considerations for model improvement would be to take in the sensor and lidar data into the model so that the model can gain a sense of distance. The model could also be trained on the hold out trip which was labeled HMB_3 in the Udacity github.