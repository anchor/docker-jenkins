FROM registry.anchor.net.au/engineering/haskell-wheezy:latest

RUN apt-get update
RUN apt-get install -y \
    advancecomp \
    build-essential \
    debhelper \
    git \
    jpegoptim \
    libssl-dev \
    m4 \
    openssh-client \
    openssh-server \
    optipng \
    rsync \
    ruby-sass \
    sudo \
    tar \
    vim \
    wget
RUN apt-get install -y --no-install-recommends openjdk-7-jdk

RUN mkdir -p /var/run/sshd

RUN adduser --quiet jenkins
RUN echo "jenkins:jenkins" | chpasswd

RUN sed -i -e '/^Defaults.*requiretty$/d' -e '/^%sudo/d' /etc/sudoers
RUN echo "%sudo ALL=(ALL) NOPASSWD : ALL" > /etc/sudoers.d/sudogroup

RUN adduser jenkins sudo

ADD public-key /home/jenkins/.ssh/authorized_keys
RUN chown -R jenkins:jenkins /home/jenkins/.ssh/ && chmod 0700 /home/jenkins/.ssh && chmod 0644 /home/jenkins/.ssh/authorized_keys
RUN ssh-keyscan -t rsa github.com >> /home/jenkins/.ssh/known_hosts
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
