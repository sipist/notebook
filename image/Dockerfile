# Copyright (c) SIPist Development Team
# Distributed under the terms of the Modified BSD License.
FROM quay.io/jupyter/scipy-notebook:2025-07-21

LABEL maintainer="Flavio Martins <flavio.f.martins@tecnico.ulisboa.pt>"
ARG NB_BUILD=0

# Fix: https://github.com/hadolint/hadolint/wiki/DL4006
# Fix: https://github.com/koalaman/shellcheck/wiki/SC3014
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER ${NB_UID}

# Install PostgreSQL
RUN mamba install --yes \
    postgresql \
    pspg && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install utils
RUN mamba install --yes \
    'bat' \
    'fd-find' \
    'file' \
    'git-delta' \
    'git-lfs' \
    'htop' \
    'jc' \
    'jq' \
    'ncdu' \
    'ripgrep' \
    'rclone' \
    'rsync' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install special extras
RUN mamba install --yes \
    'cchardet' \
    'dateparser' \
    'ftfy' \
    'html5lib' \
    'langcodes' \
    'lxml' \
    'tld' \
    'yarl' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install redis
RUN echo 'redis-server=7.2.*' >> "${CONDA_DIR}/conda-meta/pinned" && \
    mamba install --yes \
    'redis-server' \
    'redis-py' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install DuckDB and SQLalchemy driver
RUN mamba install --yes \
    'duckdb-cli' \
    'duckdb-engine' \
    'python-duckdb' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install sqlite
RUN mamba install --yes \
    'sqlite' \
    'sqldiff' \
    'sqlite_analyzer' \
    'sqlite_rsync' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install PostgreSQL Python drivers
RUN mamba install --yes \
    'psycopg' \
    'psycopg-c' \
    'psycopg-pool' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install PostgreSQL extras
RUN mamba install --yes \
    'pgcli' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install JupySQL
RUN mamba install --yes \
    'jupysql' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install utility extras
RUN mamba install --yes \
    'jupyterlab_execute_time' \
    'jupyterlab-spellchecker' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install collaboration extras
RUN mamba install --yes \
    'jupyter-archive' \
    'jupyter-collaboration' && \
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

# Install trec_eval
RUN mamba install --yes \
    'trec_eval' && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

USER ${NB_UID}

COPY --chown=${NB_UID}:${NB_GID} ./.psqlrc ${HOME}/.psqlrc
COPY --chown=${NB_UID}:${NB_GID} ./.sqliterc ${HOME}/.sqliterc

WORKDIR "${HOME}"
