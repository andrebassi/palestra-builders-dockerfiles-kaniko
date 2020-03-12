# Build to Project
FROM golang:1.14 AS build-source
WORKDIR /app
COPY ./app /app
ENV CGO_ENABLED=0
RUN go build -o main .

# Compress to binary file
FROM alpine:3.8 AS compressor
RUN apk add upx
WORKDIR /app
COPY --from=build-source /app/main /app/main
RUN upx --overlay=strip --best /app/main

# final stage
FROM alpine:3.8
WORKDIR /app
COPY --from=compressor /app/main /app/main

# Add Tini
RUN apk add --no-cache tini
ENTRYPOINT ["/sbin/tini", "--"]

# expose port
EXPOSE 8080
# app
CMD ["/app/main"]