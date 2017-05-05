FROM imriss/archlinux

RUN echo 'ManifoldLearning Julia on Arch Linux'

MAINTAINER Reza Farrahi <imriss@ieee.org>
LABEL description="ManifoldLearning Julia / Arch Linux"

RUN  pacman -Syyu --noconfirm \
  && pacman -S findutils nano vi --needed --noconfirm \
  && pacman-db-upgrade \
  && export editor=nano \
  && pacman -S --needed --noconfirm git wget gnuplot \
&& git config --global url."https://".insteadOf git:// 

# DDADD https://raw.githubusercontent.com/imriss/scylla/master/aur.sh /usr/sbin/aur.sh
# DDADD https://raw.githubusercontent.com/imriss/scylla/master/add-aur.sh /usr/sbin/add-aur
ADD ./aur.sh /usr/sbin/aur.sh
ADD ./add-aur.sh /usr/sbin/add-aur
RUN chmod u+x /usr/sbin/aur.sh
RUN chmod u+x /usr/sbin/add-aur
RUN add-aur docker

RUN su docker -c 'pacaur -S --needed --noprogressbar --noedit --noconfirm python python-pip'

RUN pip install eve \
  && pip install eve-auth-jwt

# RUN /bin/bash -c "comm -23 <(pacman -Qq) <(cat <(pactree -u julia |sort) <(pactree -u pacman |sort) <(pactree -u sudo |sort) <(pacman -Qgq base | sort) |sort -u) | xargs pacman -Rdd --noconfirm" \
RUN pacman -Scc --noconfirm \
  &&  rm /var/cache/pacman/pkg/* \
  && paccache -rf 

# RUN /bin/bash -c "du /usr/lib -hd 1 |sort -h"
# RUN /bin/bash -c "ls /usr/lib -la |sort -h"

RUN rm -rd /home/docker/sandground

