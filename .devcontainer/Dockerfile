FROM rust:latest

RUN export DEBIAN_FRONTEND="noninteractive" && \
    apt-get update && apt-get -y install --no-install-recommends \
    git \
    zsh \
    vim \
    unzip clang xserver-xorg pkg-config libgtk-3-dev curl cmake ninja-build

RUN export DEBIAN_FRONTEND="noninteractive" && \
    apt-get update && apt-get -y install --no-install-recommends \
    gcc && \
    curl -fsSL https://deb.nodesource.com/setup_16.x | bash - && \
    apt-get update && apt-get -y install --no-install-recommends \
    nodejs && \
    npm install -g n && \
    n lts && \
    n prune && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get -y install --no-install-recommends \
    yarn

WORKDIR /workdir
RUN cargo install tauri-cli
RUN export DEBIAN_FRONTEND="noninteractive" && \
    apt-get update && apt-get -y install --no-install-recommends \
    libdbus-1-3 && \
    pkg-config --libs --cflags dbus-1 && \
    apt-get -y install --no-install-recommends \
    software-properties-common && \
    apt-get update && \
    apt-get -y install --no-install-recommends \
    build-essential \
    libssl-dev \
    libayatana-appindicator3-dev \
    librsvg2-dev \
    libwebkit2gtk-4.0-dev \
    mesa-utils \
    libgl1-mesa-glx \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
ENV MESA_GL_VERSION_OVERRIDE=4.5

ENV TZ=Asia/Tokyo
RUN zsh -c "`curl -L raw.github.com/44103/dotfiles/main/install.sh`"
