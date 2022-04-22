FROM ubuntu:20.04
LABEL maintainer "Wataru MISHIMA <watal.i27e@gmail.com>"

# Ser TimeZone
ENV TZ=Asia/Tokyo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Package Install
RUN sed -i 's@archive.ubuntu.com@ftp.jaist.ac.jp/pub/Linux@g' /etc/apt/sources.list
RUN apt-get update \
 && apt-get install -y bash-completion git sudo silversearcher-ag tmux vim \
                       ethtool iproute2 iputils-ping mtr tcpdump traceroute \
                       curl iperf netcat ssh telnet wget \
 && echo "" > ~/.bashrc \
 && echo "if [ -f /etc/bash_completion ] && ! shopt -oq posix; then" >> ~/.bashrc \
 && echo "  . /etc/bash_completion" >> ~/.bashrc \
 && echo "fi" >> ~/.bashrc

# Setup Go 1.18.1
RUN curl -o ~/go1.18.1.linux-amd64.tar.gz -LO https://go.dev/dl/go1.18.1.linux-amd64.tar.gz \
    && rm -rf /usr/local/go \
    && tar -C /usr/local -xzf ~/go1.18.1.linux-amd64.tar.gz \
    && echo "export PATH=$PATH:/usr/local/go/bin" >> ~/.bashrc
