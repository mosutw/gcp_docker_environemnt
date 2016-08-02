FROM sshd_ubuntu

MAINTAINER mosu <luke1974@gmail.com>

#ADD . /data
WORKDIR /project/nodejs

# disable stdin to avoid 'dpkg-preconfigure: unable to re-open stdin'
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

RUN apt-get update  -y 
RUN apt-get install build-essential libssl-dev -y
RUN apt-get install -y apt-utils
RUN apt-get upgrade -y
RUN apt-get install -y curl
RUN apt-get install -y vim
RUN apt-get install -y locales
RUN #ln -sf /usr/share/zoneinfo/Asia/Taipei /etc/localtime
ADD locale.gen /etc/locale.gen
RUN echo "Asai/Taipei" >/etc/timezone
RUN dpkg-reconfigure --frontend noninteractive tzdata
ADD etc_locale /etc/default/locale
RUN locale-gen

# nvm and node version
ENV NVM_VERSION 0.31.2
ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 6.3.1

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v$NVM_VERSION/install.sh | bash 

RUN /bin/bash -c "source $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default"

ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/v$NODE_VERSION/bin:$PATH

EXPOSE 8080

CMD npm start
