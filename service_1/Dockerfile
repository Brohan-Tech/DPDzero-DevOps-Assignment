# Build stage
FROM golang:1.20-alpine AS builder

WORKDIR /app

COPY . .

RUN go build -o service1 main.go

# Final stage
FROM alpine

WORKDIR /app

#Install curl for healthcheck
RUN apk add --no-cache curl

COPY --from=builder /app/service1 .

CMD ["./service1"]
