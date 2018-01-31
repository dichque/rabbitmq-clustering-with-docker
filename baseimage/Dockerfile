FROM openshift/base-centos7

# Install base deps
RUN yum install -y net-tools pwgen wget curl tar unzip tail less mlocate logrotate sudo

# Install Erlang repo
# http://www.rabbitmq.com/install-rpm.html
ADD rabbitmq-erlang.repo  /etc/yum.repos.d

# Install RabbitMQ deps
RUN rpm --import https://www.rabbitmq.com/rabbitmq-signing-key-public.asc

RUN yum install -y erlang

RUN yum install -y http://www.rabbitmq.com/releases/rabbitmq-server/v3.6.15/rabbitmq-server-3.6.15-1.el7.noarch.rpm

RUN yum clean all

# Allow triggerable events on the first time running
RUN touch /tmp/firsttimerunning
