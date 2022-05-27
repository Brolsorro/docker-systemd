FROM alt:p8

RUN apt-get update
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get install -y dbus
RUN apt-get install -y systemd sysvinit-utils libsystemd

ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8   
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

CMD ["/lib/systemd/systemd"]