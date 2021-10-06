# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.187.0/containers/python-3/.devcontainer/base.Dockerfile

# [Choice] Python version: 3, 3.9, 3.8, 3.7, 3.6
ARG VARIANT="3.9"
FROM mcr.microsoft.com/vscode/devcontainers/python:0-${VARIANT}

# [Option] Install Node.js
ARG INSTALL_NODE="true"
ARG NODE_VERSION="lts/*"
RUN if [ "${INSTALL_NODE}" = "true" ]; then su vscode -c "umask 0002 && . /usr/local/share/nvm/nvm.sh && nvm install ${NODE_VERSION} 2>&1"; fi

# [Optional] If your pip requirements rarely change, uncomment this section to add them to the image.
COPY requirements.txt /tmp/pip-tmp/
RUN pip3 --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt \
    && rm -rf /tmp/pip-tmp \
    && apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends emacs-nox=1:26.1+1-3.2+deb10u2 dos2unix=7.4.0-1 uchardet=0.0.6-3 \
    && apt-get clean && rm -rf /var/lib/apt/lists/* \
    && wget --progress=dot:mega https://github.com/hadolint/hadolint/releases/download/v2.6.0/hadolint-Linux-x86_64 \
    -O /usr/bin/hadolint \
    && chmod 755 /usr/bin/hadolint \
    && wget --progress=dot:mega https://github.com/koalaman/shellcheck/releases/download/v0.7.2/shellcheck-v0.7.2.linux.x86_64.tar.xz \
    && tar xvf shellcheck-v0.7.2.linux.x86_64.tar.xz \
    && cp shellcheck-v0.7.2/shellcheck /usr/bin/ \
    && chmod 755 /usr/bin/shellcheck

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1

COPY .bashrc /tmp/.bashrc
RUN su vscode -c "cat /tmp/.bashrc >> ~/.bashrc"