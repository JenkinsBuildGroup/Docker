# ABI build infrastructure
# Docker Jenkins slave image for
# => Ubuntu Centos 7
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


FROM centos:7

# Update package repository
RUN yum -y update
RUN yum -y upgrade

# Some useful tools
RUN yum -y install curl git redhat-lsb vim wget

# Install ssh server
RUN yum -y install openssh-server wget vim git
RUN mkdir -p /var/run/sshd

# Generate keys
RUN rm -f /etc/ssh/ssh_host_dsa_key /etc/ssh/ssh_host_rsa_key && \
    ssh-keygen -q -N "" -t dsa -f /etc/ssh/ssh_host_dsa_key && \
    ssh-keygen -q -N "" -t rsa -f /etc/ssh/ssh_host_rsa_key

# Add user jenkins with password jenkins
RUN adduser jenkins
RUN echo "jenkins:jenkins" | chpasswd
RUN echo "alias ls='ls -lrgt --color'" > /home/jenkins/.bashrc

# Install sudo
RUN yum -y install sudo

# Give jenkins user passwordless 'sudo' permission restricted on apt-get
RUN echo 'jenkins ALL=(root) NOPASSWD: ALL' >> /etc/sudoers
RUN sed -i.tmp "s/Defaults    requiretty/#Defaults    requiretty/g" /etc/sudoers

# Install JRE
RUN yum -y install java-1.8.0-openjdk-headless.x86_64

# Standard SSH port
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
