FROM registry.anchor.net.au/engineering/haskell-centos:latest

RUN yum -y update
RUN yum -y install \
    git \
    java-1.7.0-openjdk \
    m4 \
    openssh-clients \
    openssh-server \
    rpm-build \
    rpmdevtools \
    sudo
RUN yum -y groupinstall 'Development Tools'
run sshd-keygen

RUN sed -i -e '/^Defaults.*requiretty$/d' -e '/^%wheel/d' -e 's/^#\s*\(%wheel.*NOPASSWD\)/\1/' /etc/sudoers 
RUN adduser jenkins -G wheel

ADD public-key /home/jenkins/.ssh/authorized_keys
RUN chown -R jenkins:jenkins /home/jenkins/.ssh/ && chmod 0700 /home/jenkins/.ssh && chmod 0644 /home/jenkins/.ssh/authorized_keys

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
