# ABI build infrastructure
# Docker Jenkins slave image for
# => Ubuntu 14.04 LTS
#
# 2016-10-25
# Philipp Thiel


#######################################################
#
# !!! IMPORTANT NOTE !!!
#
# THE DOCKER IMAGE PRODUCED BY THIS FILE IS
# *ONLY* FOR INTERNAL USE IN OUR INFRASTRUCTURE!
#
# IT CONTAINS PLAIN TEXT PASSWORDS
#
#######################################################


FROM ubuntu:14.04

# Update package repository
RUN apt-get update
RUN apt-get -y upgrade

# Some useful tools
RUN apt-get -y install curl git lsb-release vim wget

# Install ssh server
RUN apt-get -y install openssh-server
RUN mkdir -p /var/run/sshd

# Add user jenkins with password jenkins
RUN adduser --quiet jenkins
RUN echo "jenkins:jenkins" | chpasswd
RUN echo "alias ls='ls -lrgt --color'" > /home/jenkins/.bashrc

# Install sudo
RUN apt-get -y install sudo

# Give jenkins user passwordless 'sudo' permission restricted on apt-get
RUN echo 'jenkins ALL=(root) NOPASSWD: ALL' >> /etc/sudoers

# Install JRE necessary for Jenkins slave connection
RUN apt-get -y install default-jre-headless

# Standard SSH port
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
