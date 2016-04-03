FROM centos:7

ENV CONSUL_VERSION 0.6.4

RUN yum install -y wget unzip bind-utils \
  && wget https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip \
  && unzip consul_${CONSUL_VERSION}_linux_amd64.zip \
  && mv consul /bin/ \
  && rm -rf consul_${CONSUL_VERSION}_linux_amd64.zip \
  && mkdir /etc/consul.d \
  && echo '{"ports":{"dns":53}}' > /etc/consul.d/000-consul.json \
  && echo "nameserver 127.0.0.1" > /etc/resolv.conf
#  && cd /tmp \
#  && wget -O ui.zip https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_web_ui.zip \
#  && unzip ui.zip \
#  && mkdir -p /ui \
#  && mv * /ui \
#  && rm -rf /tmp/*

EXPOSE 8300 8301 8301/udp 8302 8302/udp 8400 8500 8600 8600/udp

CMD ["/bin/consul", "agent", "-server", "-bootstrap-expect", "1", "-node=server-one", "-data-dir", "/tmp", "-config-dir", "/etc/consul.d"]
