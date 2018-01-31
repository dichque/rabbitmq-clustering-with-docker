FROM jaganaga/rabbitbase
MAINTAINER Jagadish Nagarajaiah jaganaga@cisco.com

# Create directories
RUN mkdir /opt/rabbit
RUN mkdir /opt/simulator
RUN mkdir /opt/simulator/tools

# Add the files from the local repository into the container
COPY rabbitmq.config     /etc/rabbitmq/
COPY rabbitmq-env.conf   /etc/rabbitmq/
COPY erlang.cookie       /var/lib/rabbitmq/.erlang.cookie
COPY startclusternode.sh /opt/rabbit/
COPY debugnodes.sh       /opt/rabbit/
COPY tl                  /bin/tl
COPY rl                  /bin/rl
COPY rst                 /bin/rst

# Add the simulator tooling
COPY simulator_tools/start_node.sh   /opt/simulator/tools/
COPY simulator_tools/stop_node.sh    /opt/simulator/tools/
COPY simulator_tools/join_cluster.sh   /opt/simulator/tools/
COPY simulator_tools/leave_cluster.sh  /opt/simulator/tools/
COPY simulator_tools/reset_first_time_running.sh /opt/simulator/tools/

# Set the file permissions in the container
RUN chmod 644 /etc/rabbitmq/rabbitmq.config
RUN chmod 644 /etc/rabbitmq/rabbitmq-env.conf
RUN chmod 400 /var/lib/rabbitmq/.erlang.cookie
RUN chmod 755 /opt/rabbit/startclusternode.sh
RUN chmod 755 /opt/rabbit/debugnodes.sh
RUN chmod 755 /bin/tl
RUN chmod 755 /bin/rl
RUN chmod 755 /bin/rst
RUN chmod 755 /opt/simulator
RUN chmod 755 /opt/simulator/tools
RUN chmod 755 /opt/simulator/tools/start_node.sh
RUN chmod 755 /opt/simulator/tools/stop_node.sh
RUN chmod 755 /opt/simulator/tools/join_cluster.sh
RUN chmod 755 /opt/simulator/tools/leave_cluster.sh
RUN chmod 755 /opt/simulator/tools/reset_first_time_running.sh

# Set ownership permissions on files in the container
RUN chown -R rabbitmq:rabbitmq /var/lib/rabbitmq /etc/rabbitmq /tmp/firsttimerunning
RUN chmod 777 /var/lib/rabbitmq /etc/rabbitmq

# Expose ports inside the container to the host
EXPOSE 1883
EXPOSE 8883
EXPOSE 5672
EXPOSE 15672
EXPOSE 25672
EXPOSE 4369
EXPOSE 9100
EXPOSE 9101
EXPOSE 9102
EXPOSE 9103
EXPOSE 9104
EXPOSE 9105

RUN echo "rabbitmq ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER rabbitmq

# Run this to debug the cluster nodes by allowing ssh login
#CMD /opt/rabbit/debugnodes.sh

# Run this to autostart the cluster nodes
ENTRYPOINT ["/opt/rabbit/startclusternode.sh"]
