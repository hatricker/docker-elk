FROM golang:1.13-alpine AS builder

RUN apk update && apk upgrade && \
    apk add --no-cache ca-certificates bash git openssh build-base && \
    go get -v gitlab.com/hatricker/etherbeat && \
    cd /go/src/gitlab.com/hatricker/etherbeat && \
    make

FROM alpine:latest
RUN apk --no-cache add ca-certificates bash
WORKDIR /root/
COPY --from=builder /go/src/gitlab.com/hatricker/etherbeat/etherbeat* ./

ENTRYPOINT [ "/root/etherbeat" ]
CMD [ "-c", "/root/etherbeat.yml", "-e"]