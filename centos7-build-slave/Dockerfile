FROM centos:centos7

RUN yum -y install java-1.7.0-openjdk
RUN yum -y install openssh-server openssh-clients && sshd-keygen
RUN yum -y install sudo

ADD peterson-ghc.repo /etc/yum.repos.d/peterson-ghc.repo
ADD peterson-cabal-install.repo /etc/yum.repos.d/peterson-cabal-install.repo
RUN yum -y update
RUN yum -y install ghc cabal-install gcc-c++
RUN yum -y groupinstall 'Development Tools'
RUN yum -y install rpm-build rpmdevtools
RUN yum -y install git

RUN sed -i -e '/^Defaults.*requiretty$/d' -e '/^%wheel/d' -e 's/^#\s*\(%wheel.*NOPASSWD\)/\1/' /etc/sudoers 
RUN adduser jenkins -G wheel

ADD public-key /home/jenkins/.ssh/authorized_keys
RUN chown -R jenkins:jenkins /home/jenkins/.ssh/ && chmod 0700 /home/jenkins/.ssh && chmod 0644 /home/jenkins/.ssh/authorized_keys

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
