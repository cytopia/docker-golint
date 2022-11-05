FROM golang:stretch as builder

# Install dependencies
RUN set -x \
	&& DEBIAN_FRONTEND=noninteractive apt-get update -qq \
	&& DEBIAN_FRONTEND=noninteractive apt-get install -qq -y --no-install-recommends --no-install-suggests \
		git \
		gox \
	&& curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh

# Get and build golint
RUN set -x \
	&& export GOPATH=/go \
	&& mkdir -p /go/src/golang.org/x \
	&& go get -u golang.org/x/lint/golint

# Use a clean tiny image to store artifacts in
FROM alpine:3.16
LABEL \
	maintainer="cytopia <cytopia@everythingcli.org>" \
	repo="https://github.com/cytopia/docker-golint"

COPY --from=builder /go/bin/golint /usr/local/bin/golint

ENV WORKDIR /data
WORKDIR /data

ENTRYPOINT ["golint"]
CMD ["--version"]
