FROM golang:1.16.15-alpine3.15 AS builder
RUN apk --no-cache add gcc git make bash
RUN git config --global http.version HTTP/1.1
ADD . snapshot-controller
WORKDIR snapshot-controller
RUN make

FROM gcr.io/distroless/static:latest
LABEL maintainers="Kubernetes Authors"
LABEL description="Snapshot Controller"
ARG binary=./bin/snapshot-controller

COPY --from=builder ./snapshot-controller/bin/snapshot-controller  snapshot-controller
ENTRYPOINT ["/snapshot-controller"]
