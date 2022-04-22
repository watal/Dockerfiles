FROM watal/ubuntu:20.04
LABEL maintainer "Wataru MISHIMA <watal.i27e@gmail.com>"

RUN apt-get update && apt-get install -y gnupg2 \
 && curl -s https://deb.frrouting.org/frr/keys.asc | sudo apt-key add - \
 && FRRVER="frr-stable" \
 && echo deb https://deb.frrouting.org/frr $(lsb_release -s -c) $FRRVER | tee -a /etc/apt/sources.list.d/frr.list \
 && apt-get install -y frr frr-pythontools \
 && sed -i -e 's/=no/=yes/g' /etc/frr/daemons
