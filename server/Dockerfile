FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    openssh-server \
    nginx \
    git \
    && rm -rf /var/lib/apt/lists/*

RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

RUN sed -i 's/#PubkeyAuthentication yes/PubkeyAuthentication yes/' /etc/ssh/sshd_config

RUN mkdir -p /root/.ssh
RUN chmod 700 /root/.ssh

COPY github-actions-key.pub /root/.ssh/authorized_keys

RUN chmod 600 /root/.ssh/authorized_keys

RUN mkdir -p /var/www/html

WORKDIR /var/www/html

EXPOSE 80 22

CMD service ssh start && nginx -g 'daemon off;'
