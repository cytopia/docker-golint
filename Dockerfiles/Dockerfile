FROM golang:stretch as builder

RUN set -x \
	&& go install golang.org/x/lint/golint@latest

FROM alpine:3.16
LABEL \
	maintainer="cytopia <cytopia@everythingcli.org>" \
	repo="https://github.com/cytopia/docker-golint"

COPY --from=builder /go/bin/golint /usr/local/bin/golint

ENV WORKDIR /data
WORKDIR /data

ENTRYPOINT ["golint"]
CMD ["--version"]
