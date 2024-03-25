FROM ghcr.io/felipecrs/jenkins-agent-dind

ARG VERSION=stable
ARG HOST=x86_64-unknown-linux-gnu
ARG ADDITIONAL_PACKAGES=""

USER root

RUN if [ -n "$ADDITIONAL_PACKAGES" ]; then apt-get update && apt-get install -y $ADDITIONAL_PACKAGES && \
    rm -rf /var/lib/apt/lists/*; fi

USER jenkins

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y --default-toolchain $VERSION -t $HOST
ENV PATH="/home/jenkins/.cargo/bin:${PATH}"

# install some more tools
# cargo-binstall
RUN curl -L --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/cargo-bins/cargo-binstall/main/install-from-binstall-release.sh | bash
# cargo-nextest
RUN cargo binstall cargo-nextest --secure -y
# cargo-llvm-cov
RUN curl --proto '=https' --tlsv1.2 -fsSL https://github.com/taiki-e/cargo-llvm-cov/releases/latest/download/cargo-llvm-cov-x86_64-unknown-linux-gnu.tar.gz | tar xzf - -C "$HOME/.cargo/bin"
