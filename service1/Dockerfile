# Stage 1: Build
FROM golang:1.24-alpine AS builder

WORKDIR /app


COPY go.mod ./
RUN go mod download

# Copy code
COPY . .
RUN go build -o service1

# Stage 2: Runtime
FROM alpine:latest
RUN apk add --no-cache curl

WORKDIR /root/
COPY --from=builder /app/service1 .
EXPOSE 8001
CMD ["./service1"]

