FROM ubuntu:latest

RUN apt update && apt install  openssh-server sudo -y
RUN apt update && apt install  vim sudo -y
RUN apt update && apt install  r-base sudo -y

RUN useradd -m test
RUN usermod -aG sudo test

RUN mkdir -p /home/test/.ssh
RUN chown -R test:test /home/test/.ssh
COPY putty_key.pub /home/test/.ssh/authorized_keys
RUN  echo 'test:test' | chpasswd

RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/g' /etc/ssh/sshd_config
RUN sed -i 's/#ChallengeResponseAuthentication yes/ChallengeResponseAuthentication no/g' /etc/ssh/sshd_config
RUN sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config

RUN service ssh start
EXPOSE 22
CMD ["/usr/sbin/sshd","-D"]