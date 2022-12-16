# docker build -t janzi/vsts-build-agents:ubuntu-22.10-lite-buildah buildah/lite/.
FROM janzi/vsts-build-agents:ubuntu-22.10-lite

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    buildah \
 && rm -rf /var/lib/apt/lists/*
