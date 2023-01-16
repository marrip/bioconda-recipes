FROM condaforge/mambaforge:22.9.0-3
ARG USERNAME=something
ARG USER_UID=1000
ARG USER_GID=${USER_UID}
ARG FULLNAME="Your full name"
ARG MAIL="some@mail.address"
ENV DEBIAN_FRONTEND noninteractive
ENV HTTPS_PROXY http://proxy.ihelse.net:3128 
ENV HTTP_PROXY http://proxy.ihelse.net:3128 
ENV http_proxy http://proxy.ihelse.net:3128 
ENV https_proxy http://proxy.ihelse.net:3128 
ENV pip_packages "ansible"
 
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        git \
        openssh-client \
        silversearcher-ag \
        sshpass \
        fish \
        wget \
        sudo \
        vim \
    && rm -rf /var/lib/apt/lists/* \
    && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
    && apt-get clean \
    && mamba install boa \
    && groupadd --gid ${USER_GID} ${USERNAME} \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME -s /usr/bin/fish \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME 
USER ${USERNAME}
RUN git config --global pull.rebase false && \
    git config --global user.email "${MAIL}" && \
    git config --global user.name "${FULLNAME}"
