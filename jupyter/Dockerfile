FROM jupyter/minimal-notebook:latest

USER root

# Update aptitude with new repo
RUN apt-get update \
    && apt-get install -y git

# Install Wget
RUN apt-get update && apt-get install -y --no-install-recommends wget

# Install Python3 and all the requirements.txt
RUN apt-get update && apt-get install -y --no-install-recommends \
        apt-utils \
        python3-dev \
        python3-wheel \
    && pip3 install --upgrade pip

#Build Solidity compiler from source
RUN apt install -y build-essential cmake

RUN wget https://github.com/ethereum/solidity/releases/download/v0.8.4/solidity_0.8.4.tar.gz

RUN tar xvzf solidity_0.8.4.tar.gz && mv solidity_0.8.4 solidity

RUN apt-get update && \
      apt-get -y install sudo

RUN useradd -m docker && echo "docker:docker" | chpasswd && adduser docker sudo

RUN solidity/scripts/install_deps.sh
RUN solidity/scripts/build.sh

# Install Python3 and all the requirements.txt
COPY ./requirements.txt ./
RUN pip3 install -r requirements.txt