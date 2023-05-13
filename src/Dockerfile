# use -bullseye variants on local arm64/Apple Silicon
FROM mcr.microsoft.com/devcontainers/base:bullseye

COPY library-scripts/*.sh /tmp/library-scripts/

ARG INSTALL_ZSH=true
ARG UPGRADE_PACKAGES=false
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID
ARG NODE_VERSION="lts/*"
ENV NVM_DIR=/usr/local/share/nvm
ENV NVM_SYMLINK_CURRENT=true \
    PATH=${NVM_DIR}/current/bin:${PATH}
ARG TERRAFORM_VERSION=1.4.6
ARG TFLINT_VERSION=0.46.1
ARG TERRAGRUNT_VERSION=0.45.11

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && bash /tmp/library-scripts/common-debian.sh "${INSTALL_ZSH}" "${USERNAME}" "${USER_UID}" "${USER_GID}" "${UPGRADE_PACKAGES}" "true" "true" \ 
    && bash /tmp/library-scripts/azcli-debian.sh \
    && bash /tmp/library-scripts/node-debian.sh "${NVM_DIR}" "${NODE_VERSION}" "${USERNAME}" \
    && bash /tmp/library-scripts/docker-in-docker-debian.sh \
    && bash /tmp/library-scripts/terraform-debian.sh "${TERRAFORM_VERSION}" "${TFLINT_VERSION}" "${TERRAGRUNT_VERSION}" \
    && bash /tmp/library-scripts/powershell-debian.sh \
    && bash /tmp/library-scripts/go-debian.sh \
    && apt-get install -y graphviz \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/library-scripts

ENTRYPOINT [ "/usr/local/share/docker-init.sh" ]
CMD [ "sleep", "infinity" ]
