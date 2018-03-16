#
# Bootstrap Dockerfile for CentOS 7
#

FROM centos:7

MAINTAINER sl <ott321@yeah.net>
RUN
# set -x 执行指令后，会先显示该指令及所下的参数
RUN set -x \
    # Fix root terminal
    && echo "export TERM=xterm" >> /root/.bashrc \
    && yum upgrade \
         # 安装 wget
    && rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7 \
    && yum -y install wget \
    && yum install \
            autoconf \
            automake \
            binutils \
            bison \
            flex \
            gcc \
            gcc-c++ \
            gettext \
            dnf \
            dnf-plugins-core \
            yum-utils \
            libtool \
            re2c \
            make \
            patch \
            pkgconfig \
            redhat-rpm-config \
            rpm-build \
            rpm-sign \
            yum-utils \
            rpm-build \
            rpmdevtools \
            sudo \
            wget \
            git \
            gnupg \
            pygpgme \
            wget \
            ccache \
            cmake3 \
            readline-devel \
            libyaml-devel \
            binutils-devel \
            zlib-devel \
            doxygen \
            perl-Test-Harness \
            scl-utils \
            scl-utils-build \
    && yum clean all
