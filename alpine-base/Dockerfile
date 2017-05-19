FROM alpine:latest

MAINTAINER moimog33@gmail.com

# Configurable settings.
ENV TIMEZONE        Pacific/Auckland

# System settings
ENV LANG            en_US.UTF-8
ENV LC_ALL          en_US.UTF-8
ENV TERM            xterm

# Basic setup.
RUN apk update && \
    apk upgrade

# With minimal apps.
RUN apk add --update \
    git \
    bash \
    shadow \
    curl \
    wget \
    tzdata

# Set timezone.
RUN cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
    echo "${TIMEZONE}" > /etc/timezone

# Copy config.
COPY config/bashrc /root/.bashrc

# Usefull bash alias for docker exec.
RUN ln -s /bin/bash /bash && \
    ln -s /bin/sh /sh

# Cleanup.
RUN apk del tzdata && \
    rm -rf /var/cache/apk/*

# Prepare folders and set our script.
RUN mkdir -p /www && \
    mkdir /scripts && \
    chmod -R 755 /scripts
COPY ./scripts/change_uid_gid.sh /scripts/change_uid_gid.sh
RUN chmod +x /scripts/change_uid_gid.sh
COPY ./scripts/install_tools.sh /scripts/install_tools.sh
RUN chmod +x /scripts/install_tools.sh