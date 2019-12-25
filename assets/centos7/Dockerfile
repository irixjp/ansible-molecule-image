FROM centos:7

LABEL maintainer "@irix_jp"

RUN yum makecache fast && \
    yum update -y && \
    yum install -y python sudo yum-plugin-ovl bash iproute && \
    yum install -y which openssh-server && \
    yum install -y httpd && \
    sed -i 's/plugins=0/plugins=1/g' /etc/yum.conf && \
    yum clean all

ENV ANSIBLE_USER=ansible SUDO_GROUP=wheel DEPLOY_GROUP=deployer
RUN set -xe \
    && groupadd -r ${ANSIBLE_USER} \
    && groupadd -r ${DEPLOY_GROUP} \
    && useradd -m -g ${ANSIBLE_USER} ${ANSIBLE_USER} \
    && usermod -aG ${SUDO_GROUP} ${ANSIBLE_USER} \
    && usermod -aG ${DEPLOY_GROUP} ${ANSIBLE_USER} \
    && sed -i "/^%${SUDO_GROUP}/s/ALL\$/NOPASSWD:ALL/g" /etc/sudoers
