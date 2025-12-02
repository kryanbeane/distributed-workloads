ARG PYTHON_VERSION=312
ARG IMAGE_TAG=9.6-1755735361

FROM registry.access.redhat.com/ubi9/python-${PYTHON_VERSION}:${IMAGE_TAG}

ARG TARGETARCH

LABEL name="ray-ubi9-py312" \
      summary="Python 3.12 image based on UBI9 for Ray" \
      description="Python 3.12 image based on UBI9 for Ray" \
      io.k8s.display-name="Python 3.12 base image for Ray" \
      io.k8s.description="Python 3.12 image based on UBI9 for Ray" \
      authoritative-source-url="https://github.com/opendatahub-io/distributed-workloads"

# Install Python packages

# Install micropipenv to deploy packages from Pipfile.lock
RUN pip install --no-cache-dir -U "micropipenv[toml]"

# Install Python dependencies from Pipfile.lock file
COPY Pipfile.lock ./

RUN micropipenv install && rm -f ./Pipfile.lock

# Restore user workspace
USER 1001
WORKDIR /opt/app-root/src