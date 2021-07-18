FROM cloudbees/cloudbees-core-agent:2.263.1.2

USER root

#Install Epel Repo
RUN yum --disableplugin=subscription-manager -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

#Install System Depdendicies 
RUN yum --disableplugin=subscription-manager -y update \
	&& yum --disableplugin=subscription-manager -y install yum-utils \
	&& yum --disableplugin=subscription-manager -y install dnf-plugins-core \
	&& yum --disableplugin=subscription-manager -y install jq \
	&& yum --disableplugin=subscription-manager -y install wget \
	&& yum --disableplugin=subscription-manager -y install git \
	&& yum --disableplugin=subscription-manager -y install curl \
	&& yum --disableplugin=subscription-manager -y install python3 \
	&& yum --disableplugin=subscription-manager -y install python3-pip \
	&& yum clean all 

RUN unlink /usr/sbin/packer

#Upgrade and install Python modules and Ansible 
RUN pip3 install --upgrade pip
RUN pip3 install boto3
RUN pip3 install ansible

#Install Packer and Terraform
RUN yum-config-manager --add-repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo \
	&& yum --disableplugin=subscription-manager -y install packer \
	&& yum --disableplugin=subscription-manager -y install terraform \ 
	&& yum clean all  

COPY run.sh /home/run.sh
RUN chmod -R g+rwx /home && \
    chmod -R g+rwx /usr/bin && \
    chmod -R g+rwx /usr/local/bin && \
    chmod -R g+rwx /usr/share && \
    chgrp -R 0 /home && \
    chmod g+w /etc/passwd


ENTRYPOINT ["/bin/sh", "-c", "/home/run.sh" ]
