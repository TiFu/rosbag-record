# Data Collection

# Setup

0. Make sure that the PC you are running this on has USB3.0
1. Clone this repository
2. Install ros melodic: `sudo apt-get install ros-melodic-desktop-full`
3. Install librealsense
  1. For TX2: https://github.com/IntelRealSense/librealsense/blob/development/doc/installation_jetson.md
  2. For any other PC: https://github.com/IntelRealSense/librealsense/tree/development
  3. Test by running `realsense-viewer` and checking if D435 is shown as device and *transmits* both color and depth images
4. `git submodule init`
5. `git submodule update`
6. `catkin_make -DCATKIN_ENABLE_TESTING=False -DCMAKE_BUILD_TYPE=Release`

# Running

1. `source /opt/ros/melodic/setup.bash`
2. `source ./devel/setup.bash`
3. `roslaunch central record.launch`
4. MAKE SURE THAT IT DID **NOT** OUTPUT `[ WARN] [1569380541.033423016]: No RealSense devices were found!`
5. Verify that this shows a good depth image: `rosrun image_view image_view ige:=/camera/depth/image_rect_raw`
6. Verify that this shows a good color image: `rosrun image_view image_view ige:=/camera/color/image_raw`
7. Ctrl + C to end recording
8. From time to time: go to `central/rosbags/*`, run `rosbag play latest_rosbag.bag` and run the two verification steps (`image_view`) to check that the recording worked. 

**NOTE**: These verification steps are there because in our experience the Intel Driver is quite buggy - in case it does not produce the expected results, try unplugging and replugging the realsense camera. Please make sure that we won't have to ask people to redo everything due to some stupid driver bug.

**NOTE**: This records images & depth in RAW - about **30 seconds** correspond to **1GB** of data - so make sure that there is enough space on the device (e.g. by plugging in a HDD or USB stick)

# Postprocessing

1. Go to src/central/rosbags
2. `zip /tmp/rosbags.zip *.bag` (compresses to about 30% of the original size)
3. Download from TX2
4. Upload to GDrive or let me know and I'll setup a Digital Ocean droplet with enough space where you can upload the files via ssh