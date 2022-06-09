FROM watal/ubuntu:22.04
LABEL maintainer "Wataru MISHIMA <watal.i27e@gmail.com>"

SHELL ["/bin/bash", "-l", "-c"]

ENV GOBIN /usr/local/go/bin
RUN go install github.com/nttcom/pola/cmd/...@latest
