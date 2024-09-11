FROM ubuntu:23.10

RUN apt-get update && apt-get install -y \
                        git \
                        openssl \    
                        libpng16-16 \
                        libharfbuzz-bin \
                        iproute2 iputils-ping telnet iproute2 \
                        openssh-server
RUN echo 'root:rootAdmin' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g'

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

RUN echo "port=1300" >> /etc/ssh/sshd_config && echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config

RUN apt clean 
RUN rm -rf /var/lib/apt/list/*

EXPOSE 1300
RUN INTERNAL_IP=$(ip route get 1 | awk '{print $(NF-2);exit}') && export INTERNAL_IP

CMD ["bin/bash", "/etc/init.d/ssh start"]
