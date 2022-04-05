FROM alteros-base:7.5

WORKDIR /srv/app

RUN yum -y update

RUN yum clean all
ENV LANG=ru_RU.utf8
ENV LC_ALL=ru_RU.utf8

# For init Systemd
ENV container docker
RUN cd /lib/systemd/system/sysinit.target.wants/ \
    && ls | grep -v systemd-tmpfiles-setup | xargs rm -f $1

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