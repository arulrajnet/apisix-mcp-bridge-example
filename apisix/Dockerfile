FROM curlimages/curl:8.13.0 AS docker-binary

ARG DOCKER_VERSION=28.1.1
ENV DOCKER_VERSION=${DOCKER_VERSION}

# Install Docker Cli binary
RUN curl -SLO "https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKER_VERSION}.tgz" && \
    tar -xzvf "docker-${DOCKER_VERSION}.tgz" -C /tmp && \
    ls -l /tmp/docker/ && \
    rm -rf "docker-${DOCKER_VERSION}.tgz"

FROM apache/apisix:dev AS final

USER root

COPY --from=docker-binary /tmp/docker/docker /usr/local/bin/docker
