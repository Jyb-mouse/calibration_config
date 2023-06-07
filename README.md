
# calibration_config
此工程整理了所有数据采集车上的传感器之间的内外参。

## 文件夹

命名方式：车型号-车辆序号/日期，如： A12-001/20230322在20230322对应的参数。
目录结构：

        ├── config.yaml
        ├── intrinsic
        │    ├── camera-1.yaml
        │    ├── camera-2.yaml
        │    ├── lidar-1.yaml
        │    └── ...
        ├── extrinsic
        │    ├── camera-1_to_lidar-1.yaml
        │    ├── lidar-1_to_camera-1.yaml
        │    └── ...
**config.yaml**
-
该存储了当前车辆上的传感器关系图，具体如下： 

```python=
calibration_date: 2023-03-08
sensors:
  camera-1:
    intrinsic: 'camera-1.yaml'
    extrinsic:
      lidar-1: ['camera-1', 'lidar-1']
    
  lidar-1: 
    intrinsic: 'lidar-1.yaml'
    extrinsic:
      camera-1: ['lidar-1', 'camera-1']
      imu-1: ['lidar-1', 'imu-1']

  imu-1:
    intrinsic:
    extrinsic:
      camera-1: 
      lidar-1: ['imu-1', 'camera-1']
```
calibration_date：表示此次标定的日期
sensors：表示该车包含的传感器
- intrinsic的值表示当前传感器对应的内参文件在intrinsic文件夹下的名字
- extrinsic的值表示和这个传感器有连接关系的其他传感器名字以及关系
    
**intrinsic**
-
该文件夹下放了传感器的内参，以camera-1.yaml为例：
```python=
intrinsic:
- [1463.1887235131180, 0.0, 930.06369927748381]
- [0.0, 1462.9860405817967, 481.64944232730574]
- [0.0, 0.0, 1.0]
meta:
  calibration_date: 2023-03-08
  cam_type: MET-611BEV
  vehicle: A12-001
distortion: 
- [3.6790691260073891, 0.56024618101271395, 0.000029578301760834392, 0.000018976828996932809, -0.0091014135195192549,4.8930843717867001, 3.0002268960089866,0.0]
width: 1824
height: 944
```
intrinsic: 代表相机的内参矩阵
meta: 
- calibration_date: 该内参标定的时间
- cam_type: 该相机的摄像头产品型号
- vehicle: 车辆信息

distortion: 畸变参数
width: 图像宽度
height: 图像高度

**extrinsic**
-
该文件夹下放了该车两两传感器之间的外参，例如camera-1_to_lidar-1.yaml里存放了从camera-1到lidar-1的外参转换矩阵T。


>>>>>>> add 1.0.0 with five vehicles
