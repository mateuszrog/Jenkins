FROM ubuntu:18.04

EXPOSE 2222

RUN apt update && apt upgrade sudo -y

RUN apt install vim ansible openssh-server sudo -y

RUN mkdir -p /home/ubuntu

COPY setup_env.yml /home/ubuntu

CMD exec /bin/sh -c "trap : TERM INT; sleep 9999999999d & wait"

# RUN ansible-playbook --tags ubuntu /home/ubuntu/setup_env.yml
