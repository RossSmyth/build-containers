FROM debian:11 AS base

RUN apt-get update
RUN apt-get install git \
        build-essential \
        cmake \
        ninja-build \
        curl \
        unzip \
        gettext -y

ARG VERSION=stable

RUN git clone https://github.com/neovim/neovim.git --depth 1 --branch ${VERSION}

WORKDIR neovim
RUN make CMAKE_BUILD_TYPE=RelWithDebInfo install
RUN rm -rf /neovim

# Package
FROM alpine:latest AS export

# Build artifacts

COPY --from=base /usr/local/lib/nvim /usr/local/lib/nvim
COPY --from=base /usr/local/share/nvim /usr/local/share/nvim
COPY --from=base /usr/local/bin/nvim /usr/local/bin/nvim
