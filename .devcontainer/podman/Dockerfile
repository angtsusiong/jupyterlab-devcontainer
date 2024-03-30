FROM mcr.microsoft.com/devcontainers/miniconda:0.203.6-3

ARG USERNAME=vscode

ENV LANG="en_US.UTF-8" \
    TZ="Asia/Taipei" \
    TERM="xterm-256color" \
    CONDA_ENV="myenv" \
    CONDA_SCRIPT="/opt/conda/etc/profile.d/conda.sh"

RUN set -xe && \
    echo "==== Setting locale ====" && \
    update-locale LANG=${LANG} && \
    echo "==== Setting timezone ====" && \
    unlink /etc/localtime && \
    ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime && \
    echo ${TZ} > /etc/timezone

USER ${USERNAME}

WORKDIR /home/${USERNAME}

RUN set -xe && \
    echo "==== Create conda environment ====" && \
    . ${CONDA_SCRIPT} && \
    conda config --add channels conda-forge && \
    conda config --set channel_priority strict && \
    conda create -n ${CONDA_ENV} jupyterlab -y && \
    echo ". ${CONDA_SCRIPT}" >> /home/${USERNAME}/.bashrc && \
    echo "conda activate ${CONDA_ENV}" >> /home/${USERNAME}/.bashrc && \
    conda activate ${CONDA_ENV}
    