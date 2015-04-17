FROM debian:wheezy

RUN apt-get update
RUN apt-get install -y vim wget zlib1g-dev libgmp-dev git openssh-client openssh-server sudo tar libssl-dev

RUN wget http://packages.engineroom.anchor.net.au/ANCHOR-GPG-KEY
RUN apt-key add ANCHOR-GPG-KEY
RUN echo 'deb [ arch=amd64 ] http://packages.engineroom.anchor.net.au/feature/ghc/debian wheezy ghc' | sudo tee -a /etc/apt/sources.list.d/feature-ghc.list

RUN mkdir -p /var/run/sshd

RUN apt-get update
RUN apt-get install -y ghc-7.8.4 cabal-install-1.22 build-essential dpkg dpkg-dev devscripts
RUN apt-get install -y --no-install-recommends openjdk-7-jdk
RUN apt-get install -y python-stdeb # For building fleet

RUN adduser --quiet jenkins
RUN echo "jenkins:jenkins" | chpasswd

WORKDIR /usr/local/bin/
RUN ln -s /opt/ghc/7.8.4/bin/ghc
RUN ln -s /opt/ghc/7.8.4/bin/ghci
RUN ln -s /opt/ghc/7.8.4/bin/ghc-pkg
RUN ln -s /opt/ghc/7.8.4/bin/haddock
RUN ln -s /opt/ghc/7.8.4/bin/runghc
RUN ln -s /opt/ghc/7.8.4/bin/runhaskell
RUN ln -s /opt/ghc/7.8.4/bin/hsc2hs
RUN ln -s /opt/cabal/1.22/bin/cabal

RUN cabal update


RUN sed -i -e '/^Defaults.*requiretty$/d' -e '/^%sudo/d' /etc/sudoers
RUN echo "%sudo ALL=(ALL) NOPASSWD : ALL" > /etc/sudoers.d/sudogroup

RUN adduser jenkins sudo

ADD public-key /home/jenkins/.ssh/authorized_keys
RUN chown -R jenkins:jenkins /home/jenkins/.ssh/ && chmod 0700 /home/jenkins/.ssh && chmod 0644 /home/jenkins/.ssh/authorized_keys
RUN ssh-keyscan -t rsa github.com >> /home/jenkins/.ssh/known_hosts
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
