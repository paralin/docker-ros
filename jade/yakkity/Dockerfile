FROM synrobo/ubuntu:16.04

# Setup package sources
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu xenial main" > /etc/apt/sources.list.d/ros-latest.list' && \
    apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 0xB01FA116 && \
    apt-get update && \
    apt-get install -y ros-kinetic-ros-base python-rosinstall

RUN rosdep init

# Create user
RUN useradd -ms /bin/bash ros
USER ros
RUN rosdep update && \
    echo ". /opt/ros/kinetic/setup.bash" >> ~/.bashrc && \
    . /opt/ros/kinetic/setup.sh && \
    mkdir -p ~/catkin_ws/src/ && \
    cd ~/catkin_ws/src/ && \
    catkin_init_workspace && \
    cd ../ && catkin_make -j4 && \
    echo ". /home/ros/catkin_ws/devel/setup.bash" >> ~/.bashrc
