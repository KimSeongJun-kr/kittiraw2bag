# kittiraw2bag
The key feature of kittiraw2bag is its ability to add time, ring, and label fields to the LiDAR scan points in the KITTI Raw dataset, allowing for the creation of ROS bag files.   
To incorporate the time and ring information, the positions and orientations of the lasers in the HDL-64E LiDAR from the KITTI dataset were manually determined.
## Target sequences
As far as I know, the 03 sequence (2011_09_26_drive_0067) data is not provided.  
The IMU data for sequences 00, 02, 04, 05, and 06 is partially missing.
```
 Nr.     Sequence name     Start   End
 ---------------------------------------
 00: 2011_10_03_drive_0027 000000 004540
 01: 2011_10_03_drive_0042 000000 001100
 02: 2011_10_03_drive_0034 000000 004660
 03: 2011_09_26_drive_0067 000000 000800
 04: 2011_09_30_drive_0016 000000 000270
 05: 2011_09_30_drive_0018 000000 002760
 06: 2011_09_30_drive_0020 000000 001100
 07: 2011_09_30_drive_0027 000000 001100
 08: 2011_09_30_drive_0028 001100 005170
 09: 2011_09_30_drive_0033 000000 001590
 10: 2011_09_30_drive_0034 000000 001200
```
## Data organization
The data is organized in the following format:
```
/dataset/semantic_kitti/
            └── sequences  
                ├── 00  
                │   ├── poses.txt  
                │   ├── times.txt  
                │   ├── calib.txt  
                │   ├── labels  
                │   │   ├── 000000.label  
                │   │   ├── 000001.label  
                │   └── velodyne  
                │       ├── 000000.bin  
                │       ├── 000001.bin  
/dataset/raw_kitti/
            ├── 2011_09_30
            │   ├── calib_cam_to_cam.txt
            │   ├── calib_imu_to_velo.txt
            │   ├── calib_velo_to_cam.txt
            │   ├── 2011_09_30_drive_0016_extract
            │   │   ├── image_00
            │   │   │   ├── data
            │   │   │   │   ├── 0000000000.png
            │   │   │   │   ├── 0000000001.png
            │   │   │   └── timestamps.txt
            │   │   .
            │   │   .
            │   │   .
            │   │   ├── oxts
            │   │   │   ├── data
            │   │   │   │   ├── 0000000000.txt
            │   │   │   │   ├── 0000000001.txt
            │   │   │   ├── dataformat.txt
            │   │   │   └── timestamps.txt
            │   │   └── velodyne_points
            │   │       ├── data
            │   │       │   ├── 0000000000.txt
            │   │       │   ├── 0000000001.txt
            │   │       ├── timestamps_end.txt
            │   │       ├── timestamps_start.txt
            │   │       └── timestamps.txt
            │   ├── 2011_09_30_drive_0016_sync
            │   │   ├── image_00
            │   │   │   ├── data
            │   │   │   │   ├── 0000000000.png
            │   │   │   │   ├── 0000000001.png
            │   │   │   └── timestamps.txt
            │   │   .
            │   │   .
            │   │   .
            │   │   ├── oxts
            │   │   │   ├── data
            │   │   │   │   ├── 0000000000.txt
            │   │   │   │   ├── 0000000001.txt
            │   │   │   ├── dataformat.txt
            │   │   │   └── timestamps.txt
            │   │   └── velodyne_points
            │   │       ├── data
            │   │       │   ├── 0000000000.bin
            │   │       │   ├── 0000000001.bin
            │   │       ├── timestamps_end.txt
            │   │       ├── timestamps_start.txt
            │   │       └── timestamps.txt
```
## How to use
```
$ python3 kittiraw2bag.py --calib hdl-64E_calib.xml --raw_data <path/to/raw_kitti> --semantic_data <path/to/semantic_kitti/sequences> --sequence <target_sequence_num>
```
