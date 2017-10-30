# This image provides an environment for building and running Blue Jay [https://blue-jay.github.io] applications.

FROM openshift/base-centos7

MAINTAINER Anton Arapov <arapov@gmail.com>

EXPOSE 8080

ENV GO_MINOR_VERSION=9 \
    GO_PATCH_VERSION=2

ENV GO_VERSION=1.${GO_MINOR_VERSION}.${GO_PATCH_VERSION} \
    GOPATH=$HOME/go \
    GOBIN=$HOME/go/bin \
    SOURCE=$HOME/go/src/main \
	JAYCONFIG=$HOME/go/src/main/env.json \
    PATH=$PATH:$HOME/go/bin:/usr/local/go/bin

LABEL io.k8s.description="Platform for building and running Go applications" \
      io.k8s.display-name="Go ${GO_VERSION}" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,go,go1${GO_MINOR_VERSION}"

# Install Go toolchain
RUN yum install -y centos-release-scl epel-release && \
    INSTALL_PKGS="openssl git npm http-parser" && \
    yum install -y --setopt=tsflags=nodocs --enablerepo=centosplus $INSTALL_PKGS && \
    yum clean all -y && \
    (curl -L https://storage.googleapis.com/golang/go${GO_VERSION}.linux-amd64.tar.gz | \
        tar -xz -C /usr/local)

# Copy the S2I scripts from the specific language image to $STI_SCRIPTS_PATH
COPY ./s2i/ $STI_SCRIPTS_PATH

USER 1001

# Set the default CMD to print the usage of the language image
CMD $STI_SCRIPTS_PATH/usage
