FROM rosa-base:7.3

WORKDIR /srv/app

RUN yum -y update

RUN yum -y install lsb-core-noarch


RUN yum -y install glibc
RUN yum -y install dbus systemd systemd-sysv systemd-libs
RUN yum update && yum upgrade -y
RUN yum clean all

ENV LANG=ru_RU.utf8
ENV LC_ALL=ru_RU.utf8

# Enable Systemd
ENV container docker

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;

VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]