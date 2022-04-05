FROM centos-base:7.8

RUN yum install -y redhat-lsb-core redhat-lsb
RUN yum -y install dnf-plugins-core
RUN yum -y install epel-release && yum -y install lsb-core-noarch

WORKDIR /src

RUN yum -y install glibc

RUN yum -y install systemd systemd-sysv
RUN yum clean all

ENV LANG=en_US.utf8
ENV LC_CTYPE=en_US.utf8
ENV LC_ALL=en_US.utf8

# Enable Systemd
ENV container docker
RUN cd /lib/systemd/system/sysinit.target.wants/; \
    for i in *; do [ $i = systemd-tmpfiles-setup.service ] || rm -f $i; done
RUN rm -f /lib/systemd/system/multi-user.target.wants/* \
    /etc/systemd/system/*.wants/* \
    /lib/systemd/system/local-fs.target.wants/* \
    /lib/systemd/system/sockets.target.wants/*udev* \
    /lib/systemd/system/sockets.target.wants/*initctl* \
    /lib/systemd/system/basic.target.wants/* \
    /lib/systemd/system/anaconda.target.wants/* \
    /lib/systemd/system/plymouth* \
    /lib/systemd/system/systemd-update-utmp*


VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]
# CMD ["/lib/systemd/system"]