# Copyright (c) IPRist Development Team
# Distributed under the terms of the Modified BSD License.
FROM quay.io/jupyter/scipy-notebook:2024-03-18

LABEL maintainer="Flavio Martins <flavio.f.martins@tecnico.ulisboa.pt>"

# Fix: https://github.com/hadolint/hadolint/wiki/DL4006
# Fix: https://github.com/koalaman/shellcheck/wiki/SC3014
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER ${NB_UID}

# Install sqlite
RUN mamba install --yes \
    'sqlite' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install sqlpkg
RUN curl -sS https://webi.sh/sqlpkg | sh && \
    fix-permissions "/home/${NB_USER}"

# Install sqlean
RUN "/home/${NB_USER}/.local/bin/sqlpkg" install nalgeon/sqlean && \
    fix-permissions "/home/${NB_USER}"

# Install redis
RUN mamba install --yes \
    'redis-server==7.*' \
    'redis-py' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install JupySQL
RUN mamba install --yes \
    'jupysql' \
    'pgspecial==2.0.1' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install measurement extras
RUN mamba install --yes \
    'jupyter-resource-usage' \
    'jupyterlab_execute_time' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install utility extras
RUN mamba install --yes \
    'jupyter-archive' \
    'jupyterlab-spellchecker' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install Python language server
RUN mamba install --yes \
    'jupyterlab-lsp' \
    'python-lsp-server' \
    'python-lsp-ruff' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install html5lib
RUN mamba install --yes \
    'html5lib' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install lxml
RUN mamba install --yes \
    'lxml' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install yarl
RUN mamba install --yes \
    'yarl' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install elasticsearch-py
RUN mamba install --yes \
    'elasticsearch' \
    'elasticsearch-dsl' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install weaviate-client
RUN pip install --quiet --no-cache-dir \
    'weaviate-client' && \
    fix-permissions "/home/${NB_USER}"


USER ${NB_UID}

COPY --chown=${NB_UID}:${NB_GID} ./.sqliterc ${HOME}/.sqliterc

WORKDIR "${HOME}"
