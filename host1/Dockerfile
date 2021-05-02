FROM centos:7

USER root


RUN yum -y install openssh-server && \
    yum -y install sudo && \
    useradd remote_user && \
    echo "1234" | passwd remote_user  --stdin && \
    echo "%wheel	ALL=(ALL)	ALL" >> /etc/sudoers  && \
    echo "%wheel	ALL=(ALL)	NOPASSWD: ALL" >> /etc/sudoers && \
    mkdir /home/remote_user/.ssh && \
    chmod 700 /home/remote_user/.ssh && \
    usermod -aG wheel remote_user

COPY host1.pub /home/remote_user/.ssh/authorized_keys

RUN chown remote_user:remote_user -R /home/remote_user/.ssh && \
    chmod 600 /home/remote_user/.ssh/authorized_keys

RUN /usr/sbin/sshd-keygen

CMD /usr/sbin/sshd -D