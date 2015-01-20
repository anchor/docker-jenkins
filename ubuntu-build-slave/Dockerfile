FROM ubuntu:trusty

RUN apt-get update && apt-get install -y python-software-properties software-properties-common
RUN add-apt-repository -y "deb http://archive.ubuntu.com/ubuntu/ trusty main universe"
RUN add-apt-repository -y ppa:hvr/ghc && apt-get update

RUN apt-get install -y openssh-server openssh-client sudo git
RUN mkdir -p /var/run/sshd

# For jenkins
RUN apt-get install -y openjdk-7-jre-headless

# For builds
RUN apt-get install -y ghc-7.8.3 cabal-install-1.20 happy-1.19.3 alex-3.1.3
RUN apt-get install -y build-essential autoconf

RUN sed -i -Ee 's/^(%sudo.*)ALL$/\1 NOPASSWD:ALL/' /etc/sudoers
RUN adduser --quiet jenkins && adduser jenkins sudo
RUN echo "jenkins:jenkins" | chpasswd

ADD public-key /home/jenkins/.ssh/authorized_keys
RUN chown -R jenkins:jenkins /home/jenkins/.ssh/ && chmod 0700 /home/jenkins/.ssh && chmod 0644 /home/jenkins/.ssh/authorized_keys

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
