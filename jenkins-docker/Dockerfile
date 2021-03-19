FROM jenkins/jenkins:lts

USER root

# match the Docker group ID with your local docker group id (from /etc/group file)
ARG DOCKER_GROUP_ID=974

# update the docker version to the latest version. Go to https://download.docker.com/linux/static/stable/x86_64/ for the latest version
RUN mkdir -p /tmp/download && \
 curl -L https://download.docker.com/linux/static/stable/x86_64/docker-20.10.5.tgz | tar -xz -C /tmp/download && \
 rm -rf /tmp/download/docker/dockerd && \
 mv /tmp/download/docker/docker* /usr/local/bin/ && \
 rm -rf /tmp/download && \
 groupadd -g ${DOCKER_GROUP_ID} docker && \
 usermod -aG staff,docker jenkins

USER jenkins