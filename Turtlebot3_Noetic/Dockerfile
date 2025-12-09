FROM osrf/ros:noetic-desktop-full
ARG USER=user
ARG DEBIAN_FRONTEND=noninteractive

# ROS Noetic && Others
RUN apt-get update && apt-get install -y \
    ros-noetic-moveit \
    ros-noetic-ros-controllers \
    ros-noetic-gazebo-ros-control \
    ros-noetic-rosserial \
    ros-noetic-rosserial-arduino \
    ros-noetic-roboticsgroup-upatras-gazebo-plugins \
    ros-noetic-actionlib-tools \
    terminator \
    python3-pip \
    git \
    && rm -rf /var/lib/apt/lists/*

RUN rosdep init || true
RUN rosdep update

# Gazebo + Turtlebot3
RUN apt-get update && apt-get install -y \
    gazebo11 \
    ros-noetic-turtlebot3 \
    ros-noetic-turtlebot3-simulations \
    ros-noetic-turtlebot3-gazebo \
    ros-noetic-gazebo-ros \
    ros-noetic-urdf \
    ros-noetic-xacro \
    ros-noetic-rviz \
    ros-noetic-interactive-markers \
    ros-noetic-joy \
    ros-noetic-teleop-twist-joy \
    ros-noetic-teleop-twist-keyboard \
    ros-noetic-gmapping \
    ros-noetic-amcl \
    ros-noetic-map-server \
    ros-noetic-move-base \
    ros-noetic-navigation \
    ros-noetic-teb-local-planner \
    && rm -rf /var/lib/apt/lists/*

# Integrated GPU
RUN apt-get update && apt-get install -y \
    mesa-utils \
    libgl1-mesa-dri \
    libgl1 \
    libxext6 \
    libx11-6 \
    libgl1-mesa-glx \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y \
    python3-numpy \
    python3-sklearn \
    python3-scipy \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

RUN pip install rdp

# Environment Setup
RUN echo "source /opt/ros/noetic/setup.bash" >> /root/.bashrc
ENV TURTLEBOT3_MODEL=burger
ENV DISPLAY=:0
ENV QT_X11_NO_MITSHM=1
ENV LIBGL_ALWAYS_SOFTWARE=1

# Entrypoint
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD ["bash"]

WORKDIR /root
