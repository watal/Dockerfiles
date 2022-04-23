FROM watal/ubuntu:20.04
LABEL maintainer "Wataru MISHIMA <watal.i27e@gmail.com>"

SHELL ["/bin/bash", "-l", "-c"]

# APT
RUN apt-get update \
 && apt-get install -y git autoconf automake libtool make libreadline-dev texinfo \
                       pkg-config libpam0g-dev libjson-c-dev bison flex python3-pytest \
                       libc-ares-dev python3-dev python-ipaddress python3-sphinx perl \
                       install-info build-essential libsnmp-dev libcap-dev python2 libelf-dev \
                       protobuf-c-compiler libprotobuf-c-dev libzmq5 libzmq3-dev \
                       cmake libpcre2-dev kmod gnupg2

# Python
RUN curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py \
 && python2 ./get-pip.py

# libyang
RUN curl -LO https://ci1.netdef.org/browse/LIBYANG-LIBYANGV2-8/artifact/shared/Ubuntu-20.04-x86_64-Packages/libyang-tools_2.0.7-1~ubuntu20.04u1_all.deb \
 && curl -LO https://ci1.netdef.org/browse/LIBYANG-LIBYANGV2-8/artifact/shared/Ubuntu-20.04-x86_64-Packages/libyang2-dev_2.0.7-1~ubuntu20.04u1_amd64.deb \
 && curl -LO https://ci1.netdef.org/browse/LIBYANG-LIBYANGV2-8/artifact/shared/Ubuntu-20.04-x86_64-Packages/libyang2-tools_2.0.7-1~ubuntu20.04u1_amd64.deb \
 && curl -LO https://ci1.netdef.org/browse/LIBYANG-LIBYANGV2-8/artifact/shared/Ubuntu-20.04-x86_64-Packages/libyang2_2.0.7-1~ubuntu20.04u1_amd64.deb \
 && dpkg -i *.deb

# Build & Install FRR
RUN curl -s https://deb.frrouting.org/frr/keys.asc | sudo apt-key add - \
 && FRRVER="frr-8" \
 && echo deb https://deb.frrouting.org/frr $(lsb_release -s -c) $FRRVER | tee -a /etc/apt/sources.list.d/frr.list \
 && apt-get update \
 && apt-get install -y frr frr-pythontools \
 && sed -i -e 's/=no/=yes/g' /etc/frr/daemons \
 && sed -i -e 's/pathd_options="  -A 127.0.0.1"/pathd_options="  -A 127.0.0.1 -M pathd_pcep"/g' /etc/frr/daemons
