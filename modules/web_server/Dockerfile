FROM ros:melodic-ros-base-bionic

RUN apt update 

RUN ["/bin/bash", "-c", "source /opt/ros/melodic/setup.bash && rosdep update"]

RUN apt-get update

RUN apt-get install -y ipython python-rospkg python-pip

RUN pip install pyyaml

RUN mkdir -p /root/catkin_ws/src

RUN ["/bin/bash", "-c", "source /opt/ros/melodic/setup.bash && cd /root/catkin_ws && catkin_make"]

RUN cd /root/catkin_ws/src && git clone https://github.com/RobotWebTools/web_video_server.git

RUN ["/bin/bash", "-c", "source /opt/ros/melodic/setup.bash && cd /root/catkin_ws && rosdep install --from-paths src --ignore-src -r -y"]

RUN ["/bin/bash", "-c", "source /opt/ros/melodic/setup.bash && cd /root/catkin_ws && catkin_make"]

RUN ["/bin/bash", "-c", "source /opt/ros/melodic/setup.bash && source /root/catkin_ws/devel/setup.bash"]
