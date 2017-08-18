# This will automatically be built by the Jenkinsfile
# to build manually
# docker build -t containerd-dockerfile -f Dockerfile .

FROM ppc64le/ubuntu:xenial

RUN apt-get update && apt-get install -y \
	autoconf \
	automake \
	btrfs-tools \
	curl \
	g++ \
	git \
	libseccomp-dev \
	libapparmor-dev \
	libnl-3-dev \
	libnet-dev \
	libtool \
	make \
	pkg-config \
	protobuf-c-compiler \
	protobuf-compiler \
	python-minimal \
	libcap-dev \
	libaio-dev \
	libprotobuf-c0-dev \
	libprotobuf-dev \
	unzip

# Install go
RUN curl -fsSL "https://golang.org/dl/go1.8.3.linux-ppc64le.tar.gz" \
	| tar -xzC /usr/local

ENV PATH /go/bin:/usr/local/go/bin:$PATH
ENV GOPATH /go

# Install proto3
RUN set -x \
	&& mkdir -p /go/src/github.com/google \
	&& cd /go/src/github.com/google \
	&& git clone "https://github.com/google/protobuf.git" \
	&& cd protobuf \
	&& ./autogen.sh \
	&& ./configure \
	&& make \
	&& make check \
	&& make install \
	&& ldconfig

# Install runc
RUN set -x \
	&& mkdir -p /go/src/github.com/opencontainers \
	&& cd /go/src/github.com/opencontainers \
	&& git clone "https://github.com/opencontainers/runc.git" \
	&& cd runc \
	&& make runc install \
	&& cp runc /go/bin

# Set up containerd path for Jenkinsfile to clone + use
RUN set -x \
	&& mkdir -p /go/src/github.com/containerd \

