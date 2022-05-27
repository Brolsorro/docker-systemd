FROM centos:8

RUN yum -y install dnf-plugins-core && dnf config-manager --set-enabled Devel PowerTools centosplus

RUN yum -y install epel-release && yum -y install lsb-core-noarch

# For working RU language
RUN dnf install -y glibc-langpack-ru
WORKDIR /src

RUN yum clean all
ENV LANG ru_RU.UTF-8
# ENV LC_ALL ru_RU.UTF-8
ENV container docker
RUN cd /lib/systemd/system/sysinit.target.wants/; \
    for i in *; do [ $i = systemd-tmpfiles-setup.service ] || rm -f $i; done
RUN rm -f /lib/systemd/system/multi-user.target.wants/* \
    /etc/systemd/system/*.wants/* \
    /lib/systemd/system/local-fs.target.wants/* \
    /lib/systemd/system/sockets.target.wants/*udev* \
    /lib/systemd/system/sockets.target.wants/*initctl* \
    /lib/systemd/system/basic.target.wants/* \
    /lib/systemd/system/anaconda.target.wants/*

VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]