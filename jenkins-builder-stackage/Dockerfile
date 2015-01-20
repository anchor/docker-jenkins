FROM registry.anchor.net.au/engineering/haskell:latest

RUN apt-get install -y openssh-server openssh-client sudo git
RUN mkdir -p /var/run/sshd

# For jenkins
RUN apt-get install -y openjdk-7-jre-headless

# For builds
RUN apt-get install -y build-essential autoconf

RUN sed -i -Ee 's/^(%sudo.*)ALL$/\1 NOPASSWD:ALL/' /etc/sudoers
RUN adduser --quiet jenkins && adduser jenkins sudo
RUN echo "jenkins:jenkins" | chpasswd

ADD public-key /home/jenkins/.ssh/authorized_keys
RUN chown -R jenkins:jenkins /home/jenkins/.ssh/ && chmod 0700 /home/jenkins/.ssh && chmod 0644 /home/jenkins/.ssh/authorized_keys

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
