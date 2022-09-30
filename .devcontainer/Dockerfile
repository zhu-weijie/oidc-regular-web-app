# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.195.0/containers/javascript-node/.devcontainer/base.Dockerfile
# [Choice] Node.js version (use -bullseye variants on local arm64/Apple Silicon): 16, 14, 12, 16-bullseye, 14-bullseye, 12-bullseye, 16-buster, 14-buster, 12-buster
ARG VARIANT=16-bullseye
FROM mcr.microsoft.com/devcontainers/javascript-node:0-${VARIANT}

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# [Optional] Uncomment if you want to install an additional version of node using nvm
# ARG EXTRA_NODE_VERSION=10
# RUN su node -c "umask 0002 && ./usr/local/share/nvm/nvm.sh && nvm install ${EXTRA_NODE_VERSION}"

# [Optional] Uncomment if you want to install more global node modules
# RUN su node -c "npm install -g <your-package-list-here>"

ARG DOCKER_HOME="/opt/baiyuan"
ARG DOCKER_CODE="/opt/baiyuan/code"
ARG DOCKER_GROUP="baiyuan"
ARG DOCKER_USER="baiyuan"
ARG DOCKER_UID=5000

WORKDIR ${DOCKER_CODE}

RUN groupadd -g ${DOCKER_UID} ${DOCKER_GROUP} \
    && useradd -r -u ${DOCKER_UID} -g ${DOCKER_GROUP} -d ${DOCKER_HOME} ${DOCKER_USER} \
    && chown -R ${DOCKER_USER}:${DOCKER_GROUP} ${DOCKER_HOME}

RUN apt-get update && \
    apt-get install -y curl && \
    apt-get install -y sudo && \
    apt-get install -y cargo && \
    echo ${DOCKER_USER} ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/${DOCKER_USER} && \
    chmod 0440 /etc/sudoers.d/${DOCKER_USER}

# Setup env
RUN mkdir ${DOCKER_HOME}/.ssh && \
    chown -R ${DOCKER_USER} ${DOCKER_HOME}/.ssh && \
    apt-get install -y openssh-client git && \
    ssh-keyscan github.com >> ${DOCKER_HOME}/.ssh/known_hosts && \
    echo "alias docker='sudo docker'" > ${DOCKER_HOME}/.bashrc

ENV PATH "$PATH:/opt/baiyuan/.local/bin"

USER ${DOCKER_USER}

ENTRYPOINT [ "/bin/sh", "-c" ]
