FROM resin/amd64-alpine:latest

ENV GO_VERSION 1.10

RUN apk add --no-cache git gcc

RUN buildDeps='curl' \
	&& set -x \
	&& apk add --no-cache $buildDeps \
	&& mkdir -p /usr/local/go \
	&& curl -SLO "http://resin-packages.s3.amazonaws.com/golang/v$GO_VERSION/go$GO_VERSION.linux-alpine-amd64.tar.gz" \
	&& echo "367417e97a08654547e55f0d38ffb55612ffa18a4698220b58c9a1137d36dac9  go1.10.linux-alpine-amd64.tar.gz" | sha256sum -c - \
	&& tar -xzf "go$GO_VERSION.linux-alpine-amd64.tar.gz" -C /usr/local/go --strip-components=1 \
	&& rm -f go$GO_VERSION.linux-alpine-amd64.tar.gz \
	&& apk del $buildDeps

ENV GOROOT /usr/local/go
ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH

COPY go-wrapper /usr/local/bin/

CMD ["echo","'No CMD command was set in Dockerfile! Details about CMD command could be found in Dockerfile Guide section in our Docs. Here's the link: http://docs.resin.io/deployment/dockerfile"]
