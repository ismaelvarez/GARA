FROM ros:melodic-ros-base-bionic

# Thermal Processing

RUN apt update && apt install -y apt-utils curl gnupg wget git

RUN apt-get install -y cmake freeglut3-dev libusb-1.0-0-dev libudev-dev libdlib-dev python-opencv

RUN ["/bin/bash", "-c", "source /opt/ros/melodic/setup.bash && rosdep update"]

RUN apt-get update

RUN apt-get install -y ipython python-rospkg python-pip 

RUN mkdir -p /root/catkin_ws/src

RUN ["/bin/bash", "-c", "source /opt/ros/melodic/setup.bash && cd /root/catkin_ws && catkin_make"]

RUN cd /root/catkin_ws/src && git clone https://github.com/ros-perception/vision_opencv.git && cd vision_opencv && git checkout melodic

RUN cd /root/catkin_ws/src && git clone https://github.com/ros/geometry.git && cd geometry && git checkout melodic-devel

RUN cd /root/catkin_ws/src && git clone https://github.com/ismaelvarez/gara_messages.git 

RUN cd /root/catkin_ws/src && git clone https://github.com/ismaelvarez/thermal_processing.git && cd thermal_processing && git checkout develop

RUN ["/bin/bash", "-c", "source /opt/ros/melodic/setup.bash && cd /root/catkin_ws && rosdep install --from-paths src --ignore-src -r -y"]

RUN ["/bin/bash", "-c", "source /opt/ros/melodic/setup.bash && cd /root/catkin_ws && catkin_make"]

ENTRYPOINT ["/bin/bash", "-c", "source /opt/ros/melodic/setup.bash && source /root/catkin_ws/devel/setup.bash && roslaunch --wait thermal_processing thermal_processing.launch"]
