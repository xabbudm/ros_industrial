# build this file with docker build -t myimage:latest .
# https://github.com/ros-industrial/docker/blob/master/tesseract/Dockerfile

# FROM ros:noetic-ros-core

ARG ROSDISTRO=noetic
ARG ROS_BASE_TAG=noetic-perception

FROM ros:$ROS_BASE_TAG

ARG ROSDISTRO

# update the system
RUN apt-get update && \
  apt-get install -y --no-install-recommends apt-utils && \
  apt-get upgrade -y

# install dependencies
RUN apt-get install -y --no-install-recommends \
    clang \
    clang-tidy \
    lcov \
    libassimp-dev \
    libomp-dev \
    libompl-dev \
    libtinyxml-dev \
    libtinyxml2-dev \
    liboctomap-dev \
    libbullet-dev \
    libbullet-extras-dev \
    git-all \
    tar \
    wget \
    python3-pip \
    zeal \
    doxygen \
    bash-completion \
    gdb \
    vim

# install ros dependencies
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
  ros-$ROSDISTRO-octomap \
  ros-$ROSDISTRO-rviz \
  ros-$ROSDISTRO-fcl \
  ros-$ROSDISTRO-agni-tf-tools \
  ros-$ROSDISTRO-ifopt \
  ros-$ROSDISTRO-octomap-msgs \
  ros-$ROSDISTRO-industrial-robot-client \
  ros-$ROSDISTRO-moveit \
  ros-$ROSDISTRO-tf-conversions \
  ros-$ROSDISTRO-xacro \
  ros-$ROSDISTRO-joint-state-publisher* \
  ros-$ROSDISTRO-rviz-visual-tools \
  python3-catkin-tools

RUN pip install qpsolvers

RUN git config --global --add safe.directory "*" && \
    git config --global user.email "daniel.muhle@dmgmori.com" && \
    git config --global user.name "DMuhle"

# install qt dependencies for docking system and *_qt packages
RUN apt-get update && apt-get install -y libqt5svg5-dev \
  libqwt-* \
  qtbase5-private-dev   

# install compiler cache
RUN apt install ccache -y

# configure ccache to be used on build commands
RUN echo 'export PATH=/usr/lib/ccache:$PATH' >> $HOME/.bashrc

# aliases for development
RUN echo 'alias s="git status"' >> /root/.bashrc

# source ros environment
RUN echo 'source /ros_entrypoint.sh ' >> /root/.bashrc

# gurobi
# RUN echo 'export GUROBI_HOME="/opt/gurobi952/linux64"' >> /root/.bashrc && \
#   echo 'export PATH="$PATH:$GUROBI_HOME/bin"' >> /root/.bashrc && \
#   echo 'export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:$GUROBI_HOME/lib"' >> /root/.bashrc && \
#   echo 'export GRB_LICENSE_FILE="/opt/gurobi952/gurobi.lic"' >> /root/.bashrc

ENV PKG_CONFIG_PATH /opt/ros/$ROSDISTRO/lib/pkgconfig
ENV LD_LIBRARY_PATH /opt/ros/$ROSDISTRO/lib

CMD ['bash']
