# Data Collection


# Setup

1. Clone this repository
2. `catkin_make -DCATKIN_ENABLE_TESTING=False -DCMAKE_BUILD_TYPE=Release`\


# Running

1. `source /opt/ros/melodic/setup.bash`
2. `source ./devel/setup.bash`
3. `roslaunch central record.launch`

**NOTE**: This records images & depth in RAW - about 30 seconds of clip correspond to 1GB of data - so make sure that there is enough space on the device (e.g. by plugging in a HDD or USB stick)

# Postprocessing

1. go to src/central/rosbags
2. `zip /tmp/rosbags.zip *.bag` (compresses to about 30% of the original size)