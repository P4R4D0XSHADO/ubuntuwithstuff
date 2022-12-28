FROM kasmweb/core-ubuntu-focal:1.12.0
USER root

ENV HOME /home/kasm-default-profile
ENV STARTUPDIR /dockerstartup
ENV INST_SCRIPTS $STARTUPDIR/install
WORKDIR $HOME

######### Customize Container Here ###########
RUN echo "#!/bin/bash\n\$@" > /usr/bin/sudo
RUN chmod +x /usr/bin/sudo

RUN apt update
RUN apt -y upgrade
RUN apt -y install filezilla
RUN apt -y install wireshark
RUN apt -y install nmap
RUN apt -y install default-jdk
RUN apt -y install curl
RUN apt-get -y install lynis
RUN apt -y install git
RUN apt-get -y install ruby-full

COPY assets/mrrobot.jpg /usr/share/extra/backgrounds/bg_default.png

RUN wget "https://maltego-downloads.s3.us-east-2.amazonaws.com/linux/Maltego.v4.3.1.deb"
RUN dpkg -i Maltego.v4.3.1.deb

RUN git clone https://github.com/beefproject/beef
RUN cd beef && yes | ./install


######### End Customizations ###########

RUN chown 1000:0 $HOME
RUN $STARTUPDIR/set_user_permission.sh $HOME

ENV HOME /home/kasm-user
WORKDIR $HOME
RUN mkdir -p $HOME && chown -R 1000:0 $HOME

USER 1000