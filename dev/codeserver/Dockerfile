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