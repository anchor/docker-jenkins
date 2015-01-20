FROM debian:wheezy

RUN apt-get update

RUN apt-get install -y openssh-server
RUN mkdir -p /var/run/sshd

RUN apt-get install -y --no-install-recommends openjdk-7-jdk

RUN adduser --quiet jenkins
RUN echo "jenkins:jenkins" | chpasswd

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
