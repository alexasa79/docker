FROM scratch
MAINTAINER Oracle Linux Product Team <ol-ovm-info_ww@oracle.com>
ADD oraclelinux-7.3-rootfs.tar.xz /

RUN yum groups mark convert
RUN yum group install -y "Development Tools"
RUN rpm --import https://mirror.go-repo.io/centos/RPM-GPG-KEY-GO-REPO
RUN curl -s https://mirror.go-repo.io/centos/go-repo.repo | tee /etc/yum.repos.d/go-repo.repo
RUN yum install -y golang
RUN yum install -y sudo
RUN yum install -y libcap-devel
RUN yum install -y openssl-devel

RUN groupadd sasha
RUN useradd -r -u 501 -g sasha -m sasha
RUN mkdir /home/sasha/.ssh
COPY id_rsa /home/sasha/.ssh/
COPY id_rsa.pub /home/sasha/.ssh/
RUN chown -R sasha:sasha /home/sasha
RUN echo "sasha ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/sasha
RUN chmod 0440 /etc/sudoers.d/sasha

WORKDIR /home/sasha
ENTRYPOINT /bin/bash
