# DOCKER-VERSION 1.0.0
#
# Ceph Daemon
#
# VERSION 0.0.1

#FROM ceph/base:tag-build-master-hammer-centos-7
FROM dockerhub.uniswdc.com/ceph/base:0.94.3 
MAINTAINER Sébastien Han "seb@redhat.com"

# Add bootstrap script
ADD ./daemon/entrypoint.sh /entrypoint.sh
ADD ./daemon/remove-mon.sh /remove-mon.sh
ADD ./daemon/config.*.sh /

ADD  ./daemon/my_init/my_init /sbin/my_init
RUN chmod +x /sbin/my_init
RUN mkdir -p /etc/container_environment

ADD  ./daemon/2.sh /etc/runit/2
RUN chmod +x /etc/runit/2

# add  ceph  home
RUN echo "ceph:x:167:167:Ceph daemons:/var/lib/ceph:/sbin/nologin"  >>/etc/passwd


# Add templates for confd
ADD ./daemon/confd/templates/* /etc/confd/templates/
ADD ./daemon/confd/conf.d/* /etc/confd/conf.d/
ADD ./daemon/check_zombie_mons.py /check_zombie_mons.py

# Add volumes for Ceph config and data
VOLUME ["/etc/ceph","/var/lib/ceph"]

# Execute the entrypoint
WORKDIR /
ENTRYPOINT ["/entrypoint.sh"]
