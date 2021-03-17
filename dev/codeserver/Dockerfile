FROM linuxserver/code-server:latest

# error repository 삭제
RUN rm -f /etc/apt/sources.list.d/*
RUN sudo apt-get update

RUN sudo apt-get install -y docker.io
RUN sudo apt-get install -y openjdk-11-jdk
RUN sudo apt-get install -y maven
RUN sudo apt-get install -y nodejs

# kubectl 설치
RUN sudo apt-get install -y apt-transport-https
RUN curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
RUN echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
RUN sudo apt-get update
RUN sudo apt-get install -y kubectl

# Kustomize
RUN curl -s "https://raw.githubusercontent.com/kubernetes-sigs/kustomize/master/hack/install_kustomize.sh" | bash

# aws cli
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
RUN sudo apt-get install -y unzip
RUN unzip awscliv2.zip
RUN sudo ./aws/install

# chrome
RUN curl -s https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
RUN sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
RUN sudo apt-get update
RUN sudo apt-get install -y google-chrome-stable
RUN ls /etc/apt/sources.list.d/google*
RUN sudo rm -rf /etc/apt/sources.list.d/google.list

