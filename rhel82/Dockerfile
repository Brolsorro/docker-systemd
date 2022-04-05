FROM rhel-base:8.2

WORKDIR /srv/app

COPY ./centos.repo /srv/app/
RUN rpm --import https://www.centos.org/keys/RPM-GPG-KEY-CentOS-Official \
    && cp centos.repo /etc/yum.repos.d/ && yum -y install epel-release && yum -y repolist
RUN yum repolist all

RUN yum install -y redhat-lsb-core redhat-lsb

RUN yum clean all

ENV LANG ru_RU.UTF-8
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
    /lib/systemd/system/anaconda.target.wants/*

VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]