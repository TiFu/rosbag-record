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
6. `catkin_make -DCATKIN_ENABLE_TESTING=False -DCMAKE_BUILD_TYPE=Release`\


# Running

1. `source /opt/ros/melodic/setup.bash`
2. `source ./devel/setup.bash`
3. `roslaunch central record.launch`

**NOTE**: This records images & depth in RAW - about 30 seconds of clip correspond to 1GB of data - so make sure that there is enough space on the device (e.g. by plugging in a HDD or USB stick)

# Postprocessing

1. Go to src/central/rosbags
2. `zip /tmp/rosbags.zip *.bag` (compresses to about 30% of the original size)
3. Download from TX2
4. Upload to GDrive or let me know and I'll setup a Digital Ocean droplet with enough space where you can upload the files via ssh