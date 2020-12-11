FROM ubuntu:latest

RUN apt-get update && DEBIAN_FRONTEND="noninteractive" apt-get install -y openssh-server xrdp xfce4 xfce4-power-manager xfce4-terminal sudo && apt-get clean
RUN mkdir /var/run/sshd
RUN adduser --disabled-password --gecos '' vagrant
RUN adduser vagrant sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
RUN chown -R vagrant /home/vagrant
RUN echo 'vagrant:vagrant' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN echo "xfce4-session" > /home/vagrant/.xsession

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

EXPOSE 22
EXPOSE 3389
CMD ["/usr/sbin/sshd", "-D"]
