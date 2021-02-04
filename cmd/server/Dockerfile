FROM golang:1.13-alpine
ADD . /go/src/monitoring-poc
ADD ./vendor /go/src/monitoring-poc/vendor
RUN go install monitoring-poc

FROM alpine:latest
COPY --from=0 /go/bin/monitoring-poc .
ENV PORT 8080
ENV DD_AGENT_HOST 10.225.230.6
CMD ["./monitoring-poc"]
