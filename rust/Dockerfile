FROM jenkins/agent

ARG VERSION=stable
ARG HOST=x86_64-unknown-linux-gnu
ARG ADDITIONAL_PACKAGES=""

USER root
RUN apt-get update && apt-get install -y curl build-essential $ADDITIONAL_PACKAGES && \
    rm -rf /var/lib/apt/lists/*

USER jenkins

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y --default-toolchain $VERSION --default-host $HOST
ENV PATH="/home/jenkins/.cargo/bin:${PATH}"

RUN rustc --version && cargo --version
