FROM centos 

RUN yum install -y openssh-server

RUN useradd centos_user  && \
    echo "sifra123" | passwd centos_user --stdin && \
    mkdir /home/centos_user/.ssh && \
    chmod 700 /home/centos_user/.ssh

COPY remote-key.pub /home/centos_user/.ssh/authorized_keys

RUN chown centos_user:centos_user -R /home/centos_user && \
    chmod 600 /home/centos_user/.ssh/authorized_keys

RUN /usr/sbin/sshd-keygen

CMD /usr/sbin/sshd -D