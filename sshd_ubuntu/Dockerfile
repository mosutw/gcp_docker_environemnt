FROM ubuntu:latest

MAINTAINER mosu

RUN apt-get update

#install sshd
RUN apt-get install -y openssh-server
RUN mkdir -p /var/run/sshd
#RUN mkdir -p /root/.ssh
RUN echo 'root:630418'| chpasswd

#取消pam限制
#RUN sed -ri 's/session    required    pam_loginuid.so/#session    required    pam_loginuid.so/g' /etc/pam.d/sshd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo  "export VISIBLE=now" >> /etc/profile

#複製設定檔到相對應位置, 並賦予shell script 執行權限
#ADD authorized_keys /root/.ssh/authorized_keys
ADD run.sh /run.sh
RUN chmod 755 /run.sh

#設定開放連接埠
EXPOSE 22

CMD ["/run.sh"]
