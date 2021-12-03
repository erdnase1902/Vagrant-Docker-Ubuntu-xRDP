FROM ubuntu:latest

RUN apt-get update && DEBIAN_FRONTEND="noninteractive" apt-get install -y net-tools iputils-ping software-properties-common curl zip python3 python3-pip tmux git htop build-essential aria2 openssh-server xrdp xfce4* sudo vim firefox && apt-get clean
RUN mkdir /var/run/sshd
RUN adduser --disabled-password --gecos '' vagrant
RUN adduser vagrant sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
RUN chown -R vagrant /home/vagrant
RUN echo 'vagrant:vagrant' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
USER vagrant
RUN echo "xfce4-session" > /home/vagrant/.xsession
USER root
# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
USER vagrant
RUN cd /home/vagrant && aria2c -q "https://download.jetbrains.com/product?code=PCC&latest&distribution=linux" && tar xf *.tar.gz && rm *.tar.gz
RUN cd /home/vagrant && aria2c -q "https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip" && unzip ngrok-stable-linux-amd64.zip && rm ngrok-stable-linux-amd64.zip
USER root
RUN cd /home/vagrant && aria2c -q "https://go.microsoft.com/fwlink/?LinkID=760868" && DEBIAN_FRONTEND="noninteractive" apt install ./*.deb && rm *.deb && apt-get clean
RUN curl https://get.docker.com/ | bash
RUN usermod -aG docker vagrant
EXPOSE 1-65535
CMD service docker start; /usr/sbin/sshd -D
