FROM centos:7

ENV CONSUL_VERSION 0.6.4

RUN yum install -y wget unzip bind-utils httpd php \
  && wget https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip \
  && unzip consul_${CONSUL_VERSION}_linux_amd64.zip \
  && mv consul /bin/ \
  && rm -rf consul_${CONSUL_VERSION}_linux_amd64.zip \
  && mkdir /etc/consul.d \
  && echo '{"service": {"name": "web", "tags": ["php"], "port": 80}}' > /etc/consul.d/web.json \
  && echo "<?php echo print_r(\$_SERVER[\"SERVER_ADDR\"]);" > /var/www/html/index.php \
  && chown apache:apache /var/www/html/index.php

# Simple startup script to avoid some issues observed with container restart
ADD run-httpd.sh /usr/local/bin/run-httpd
RUN chmod -v +x /usr/local/bin/run-httpd

EXPOSE 8300 8301 8301/udp 8302 8302/udp 8400 8500 8600 8600/udp 80

CMD ["run-httpd"]
