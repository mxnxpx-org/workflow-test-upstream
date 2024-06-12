# Based off of ARC's ubuntu image
# https://github.com/actions/actions-runner-controller/blob/master/runner/actions-runner.ubuntu-22.04.dockerfile
FROM ubuntu:22.04

ARG RUNNER_USER_UID=1001

RUN apt-get update -y \
    && apt-get install -y git curl sudo unzip zip jq

RUN adduser --disabled-password --gecos "" --uid $RUNNER_USER_UID runner \
    && usermod -aG sudo runner \
    && echo "%sudo   ALL=(ALL:ALL) NOPASSWD:ALL" > /etc/sudoers

ENV HOME=/home/runner

RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
    && unzip awscliv2.zip \
    && ./aws/install

# Add the Python "User Script Directory" to the PATH
ENV PATH="${PATH}:${HOME}/.local/bin/"
ENV ImageOS=ubuntu22

RUN echo "PATH=${PATH}" > /etc/environment \
    && echo "ImageOS=${ImageOS}" >> /etc/environment

USER runner

ENTRYPOINT ["/bin/bash"]
