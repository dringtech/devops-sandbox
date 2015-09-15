FROM centos:7
MAINTAINER giles@dringtech.com

EXPOSE 80

RUN curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | bash
RUN yum install -y curl openssh-server postfix gitlab-ce ruby rake postgresql
RUN chmod 775 /etc/gitlab
COPY gitlab.rb /etc/gitlab/

VOLUME [ "/etc/gitlab", "/var/log/gitlab", "/var/opt/gitlab", "/opt/gitlab/etc" ]


#    systemctl enable sshd && \
#    systemctl start sshd && \
#    systemctl enable postfix && \
#    systemctl start postfix && \
#    firewall-cmd --permanent --add-service=http && \
#    systemctl reload firewalld
