FROM ubuntu:22.04

ENV TARGETARCH="linux-x64"

ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

WORKDIR /adoagent_build_scripts/

RUN \
    apt update -y && \
    apt upgrade -y && \
    apt install -y \
        ca-certificates \
        curl \
        # dos2unix \
        # dotnet-sdk-6.0 \
        # dotnet-sdk-7.0 \
        # dotnet-sdk-8.0 \
        git \
        git-lfs \
        jq \
        libicu70 \
        # openjdk-21-jdk \
        python3.10 \
        python3-pip \
        unzip \
        wget \
        zip && \
    apt autoremove -y && apt autoclean && apt clean

RUN \
    pip3 install --upgrade pip && \
    git lfs install


# Install Azure CLI
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

WORKDIR /azp/

COPY ./start.sh ./
RUN chmod +x ./start.sh

ENV AGENT_ALLOW_RUNASROOT="true"
ENTRYPOINT ["./start.sh"]