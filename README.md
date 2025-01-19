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


## Data Dictionary
The data was collected from the Udacity open source self driving car [github](https://github.com/udacity/self-driving-car/tree/master/datasets/CH2).

Fix Information

| Information | Data Type | Description | Notes |
|---|---|---|---|
|`Time`|`float`|Time point the data was collected|Rounded to the fourth decimal place, which loses some data but allows the images to be matched to the data.|
|`latitude`|`float`|Represents the north-south position on the Earth's surface, ranging from -90° at the South Pole to +90° at the North Pole.|Positive values mean Northern Hemisphere.|
|`longitude`|`float`|Represents the east-west position, with values ranging from -180° to +180°|Positive values indicate locations east of the Prime Meridian.|
|`altitude`|`float`|The height above sea level (in meters).|---|

Vehicle Braking Information

| Information | Data Type | Description | Notes |
|---|---|---|---|
|`Time`|`float`|Time point the data was collected|Rounded to the fourth decimal place, which loses some data but allows the images to be matched to the data.|
|`brake_torque_request`|`float`|Amount of braking force the car system intends to supply.|This may be dropped later|
|`brake_torque_actual`|`float`|The real braking force applied by the vehicle.|---|
|`wheel_torque_actual`|`float`|The rotational force at the wheels that results from various inputs, such as braking, acceleration, or other mechanical forces.|---|
|`accel_over_ground`|`float`|How fast the vehicle is changing its speed in the horizontal direction|---|

Vehicle Throttle Information

| Information | Data Type | Description | Notes |
|---|---|---|---|
|`Time`|`float`|Time point the data was collected|Rounded to the fourth decimal place, which loses some data but allows the images to be matched to the data.|
|`throttle_pc`|`float`|How much the accelerator pedal is being pressed in percent.|---|
|`throttle_rate`|`float`|The rate in precent that the throttle position is changing.|---|
|`engine_rpm`|`float`|The speed at which the engine's crankshaft is rotating.|---|

Vehicle Steering Information

| Information | Data Type | Description | Notes |
|---|---|---|---|
|`Time`|`float`|Time point the data was collected|Rounded to the fourth decimal place, which loses some data but allows the images to be matched to the data.|
|`steering_wheel_angle`|`float`|The angle at which steering wheel is turned.|---|
|`steering_wheel_torque`|`float`|The amount of force being applied to turn the steering wheel.|---|
|`speed`|`float`|The vechile's speed in meters per second.|This was manipulated to kilometers per hour.|

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

### Software
| Library | Module | Purpose |
| --- | --- | --- |
| `numpy` || Ease of basic aggregate operations on data.|
| `pandas` || Read our data into a DataFrame, clean it, engineer new features, and write it out to submission files.|
| `sklearn` | | |
|  | `model_selection`| `train_test_split` for splitnting the data to test models on unseen data.|
| `os` | | Access operating level commands within python.|
| `random` | | To generate random seeds for easier analysis of models.|
| `gc` |  | To recover RAM used to save variables. |
| `joblib` | | `load` to load in saved variables.|
| | | `dump` to save variables for later use.|

## Executive Summary

### Purpose


### Data Handling


### Analysis


### Findings and Implications


### Next Steps
