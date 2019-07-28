FROM alpine:20190707
LABEL maintainer="KenjiTakahashi <kenji.sx>"

COPY sshd_config.append.tpl /etc/ssh/

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
    apk add --no-cache \
    bash \
    busybox-suid \
    curl \
    git \
    iproute2 \
    htop \
    less \
    openssh \
    ranger \
    rsync \
    util-linux \
    vim \
    zsh \
    && \
    rm -rf /etc/ssh/*key* && \
    addgroup -g 1100 rancher && \
    addgroup -g 1101 docker && \
    adduser -D -u 1100 -g rancher -G rancher -s /bin/zsh rancher && \
    adduser rancher wheel && \
    adduser rancher docker && \
    adduser -D -u 1101 -g docker -G docker -s /bin/bash docker && \
    sed -i 's/rancher:!/rancher:*/g' /etc/shadow && \
    sed -i 's/docker:!/docker:*/g' /etc/shadow && \
    ln -s /bin/ps /usr/bin/ps && \
    cat /etc/ssh/sshd_config > /etc/ssh/sshd_config.tpl && \
    cat /etc/ssh/sshd_config.append.tpl >> /etc/ssh/sshd_config.tpl && \
    rm -f /etc/ssh/sshd_config.append.tpl /etc/ssh/sshd_config

ENTRYPOINT ["/usr/bin/ros", "entrypoint"]
