# ROS1 Noetic
### Environment setup
- Ubuntu 20.04 Focal Fossa [iso](https://releases.ubuntu.com/focal/) | [wsl](https://apps.microsoft.com/detail/9mttcl66cpxj?hl=en-US&gl=US)
- ROS1 Noetic [install](https://wiki.ros.org/noetic/Installation/Ubuntu)

### Dependencies installation
1. ROS Noetic
```
sudo apt-get install -y ros-kinetic-navigation
sudo apt-get install -y ros-kinetic-robot-localization
sudo apt-get install -y ros-kinetic-robot-state-publisher
```
```
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
2. GTSAM
```
sudo add-apt-repository ppa:borglab/gtsam-release-4.0
sudo apt install libgtsam-dev libgtsam-unstable-dev
```
3. Make a working directory `ROS/src`
```
mkdir -p ROS/src
cd ROS/src/
```
4. Clone LIO-SAM repo
```
git clone https://github.com/TixiaoShan/LIO-SAM.git
cd ..
```
5. **Noetic build error fix!!!**
- Configure the utility.h (`src\LIO-SAM\include\utility.h`) to use  `#include <opencv2/opencv.hpp>`  instead of  `#include <opencv/cv.h>`
- Configure CMakeLists.txt (`src\LIO-SAM\CMakeLists.txt`) to use  `set(CMAKE_CXX_FLAGS "-std=c++14")`  instead of  `set(CMAKE_CXX_FLAGS "-std=c++11")`
- In `utility.h` file, move  `#include <opencv2/opencv.hpp>`  after the  `pcl`  headers.

6. Build
```
source /home/atom-focal/ROS/devel/setup.bash
catkin_make
```

### Running Dataset
Sample dataset from LIO-SAM
-   **Walking dataset:**  [[Google Drive](https://drive.google.com/drive/folders/1gJHwfdHCRdjP7vuT556pv8atqrCJPbUq?usp=sharing)]
-   **Park dataset:**  [[Google Drive](https://drive.google.com/drive/folders/1gJHwfdHCRdjP7vuT556pv8atqrCJPbUq?usp=sharing)]
-   **Garden dataset:**  [[Google Drive](https://drive.google.com/drive/folders/1gJHwfdHCRdjP7vuT556pv8atqrCJPbUq?usp=sharing)]

1.  Run the launch file:

```
roslaunch lio_sam run.launch
```

2.  Play existing bag files:

```
rosbag play park_dataset.bag -r 3
```
