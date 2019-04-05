FROM golang:alpine AS binarybuilder
RUN apk add --no-cache --no-progress --virtual git
RUN go get -u github.com/gogs/gogs
WORKDIR /go/src/github.com/gogs/gogs
#RUN go build

#FROM alpine:latest
#RUN addgroup -S gogs
#RUN adduser -S -g 'Gogs' -G gogs -s /bin/sh git
#WORKDIR /home/git
#COPY --chown=git:gogs --from=binarybuilder /go/src/github.com/gogs/gogs/gogs .

ENTRYPOINT ["sh"]
