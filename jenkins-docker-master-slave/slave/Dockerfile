FROM ubuntu:16.04

# Install Docker CLI
RUN apt-get update && apt-get install -y \
	apt-transport-https \
	ca-certificates curl \
    	gnupg-agent \
    	software-properties-common \
 &&  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - \
 &&  apt-key fingerprint 0EBFCD88 \
 &&  add-apt-repository \
	"deb [arch=amd64] https://download.docker.com/linux/ubuntu \
	$(lsb_release -cs) \
	stable" \
 && apt-get update \
 && apt-get install docker-ce docker-ce-cli containerd.io -y \
 && apt-get update && apt-get install -y openjdk-8-jre curl python python-pip git \
 && easy_install jenkins-webapi \
# Get docker-compose in the agent container
 && curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose && chmod +x /usr/local/bin/docker-compose \
 && mkdir -p /home/jenkins \
 && mkdir -p /var/lib/jenkins

ADD slave.py /var/lib/jenkins/slave.py

WORKDIR /home/jenkins

ENV JENKINS_URL "http://localhost:8080"
ENV JENKINS_SLAVE_ADDRESS ""
ENV JENKINS_USER "admin"
ENV JENKINS_PASS "admin"
ENV SLAVE_NAME ""
ENV SLAVE_SECRET ""
ENV SLAVE_EXECUTORS "1"
ENV SLAVE_LABELS "docker"
ENV SLAVE_WORING_DIR ""
ENV CLEAN_WORKING_DIR "true"

CMD [ "python", "-u", "/var/lib/jenkins/slave.py" ]
