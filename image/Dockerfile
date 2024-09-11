FROM ubuntu:23.10

RUN apt-get update && apt-get install -y \
                        git \
                        openssl \    
                        libpng16-16 \
                        libharfbuzz-bin \
                        iproute2
RUN apt install openssh-server
RUN apt clean 
RUN rm -rf /var/lib/apt/list/*
RUN echo "root:rootAdmin" | chpasswd

RUN INTERNAL_IP=$(ip route get 1 | awk '{print $(NF-2);exit}') && export INTERNAL_IP
