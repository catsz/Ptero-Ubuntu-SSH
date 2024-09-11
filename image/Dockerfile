FROM ubuntu:23.10

RUN apt-get update && apt-get install -y \
                        git \
                        openssl \    
                        libpng16-16 \
                        libharfbuzz-bin \
                        iproute2 iputils-ping telnet iproute2 \
                        openssh-server
RUN echo 'root:rootAdmin' | chpasswd
RUN sed -i 's/port=1300/PasswordAuthentication yes/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g'

RUN apt clean 
RUN rm -rf /var/lib/apt/list/*

EXPOSE 1300
RUN INTERNAL_IP=$(ip route get 1 | awk '{print $(NF-2);exit}') && export INTERNAL_IP
