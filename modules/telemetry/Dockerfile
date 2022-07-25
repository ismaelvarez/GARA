FROM ros:melodic-ros-base-bionic

# Gara Telemetry

RUN apt update && apt install -y apt-utils curl gnupg wget git

RUN apt install -y python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential python3-pip python3-pytest-cov  python3-setuptools

RUN python3 -m pip install -U \
  pytest-repeat \
  pytest-rerunfailures \
  pytest \
  catkin_pkg \
  catkin_tools 

RUN mkdir -p /root/catkin_ws/src

RUN ["/bin/bash", "-c", "source /opt/ros/melodic/setup.bash && cd /root/catkin_ws && catkin_make"]

RUN cd /root/catkin_ws/src && git clone https://github.com/ismaelvarez/gara_messages.git

RUN cd /root/catkin_ws/src && git clone https://github.com/ismaelvarez/gara_telemetry.git

RUN cd /root/catkin_ws/src && git clone https://github.com/RobotnikAutomation/robotnik_msgs.git && cd robotnik_msgs && git checkout melodic-devel

RUN ["/bin/bash", "-c", "source /opt/ros/melodic/setup.bash && cd /root/catkin_ws && rosdep install --from-paths src --ignore-src -r -y"]

RUN ["/bin/bash", "-c", "source /opt/ros/melodic/setup.bash && cd /root/catkin_ws && catkin_make"]

ENTRYPOINT ["/bin/bash", "-c", "source /opt/ros/melodic/setup.bash && source /root/catkin_ws/devel/setup.bash && rosrun gara_telemetry telemetry.py"]
