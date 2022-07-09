FROM ubuntu:18.04
ENV DEBIAN_FRONTEND "noninteractive"

RUN apt-get update -y

# Install utilities
RUN apt-get install -y --no-install-recommends \
  dconf-tools \
  apt-transport-https software-properties-common ppa-purge apt-utils \
  ca-certificates git curl wget \
  tar zip unzip zlib1g-dev bzip2 libbz2-dev \
  openssl libssl-dev \
  zsh vim screen tree htop \
  net-tools lynx iftop traceroute \
  yum \
  sudo

## Install gcc
RUN apt update
RUN apt install build-essential -y

ENV LANGUAGE=C.UTF-8
ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8
ENV LC_CTYPE=C.UTF-8

RUN apt-get install -y -f
RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get dist-upgrade -y

RUN apt-get install -y libsdl2-dev libsdl2-image-dev libsdl2-mixer-dev libsdl2-net-dev libsdl2-ttf-dev

RUN apt-get clean -y
RUN apt-get autoremove -y
RUN apt-get autoclean -y
RUN rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/*

ARG user_name=ubuntu
ARG user_id=1942
ARG group_name=ubuntu
ARG group_id=1942

RUN groupadd -g ${group_id} ${group_name}
RUN useradd -u ${user_id} -g ${group_id} -d /home/${user_name} --create-home --shell /usr/bin/zsh ${user_name}
RUN echo "${user_name} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
RUN chown -R ${user_name}:${group_name} /home/${user_name}
RUN chsh -s /usr/bin/zsh ${user_name}

USER ${user_name}
WORKDIR /home/${user_name}
ENV HOME /home/${user_name}

# rust
ENV RUST_VERSION stable
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain ${RUST_VERSION}
ENV PATH $PATH:$HOME/.cargo/bin
