FROM golang:alpine AS builder

WORKDIR /go/src/app

# Get Reflex for live reload in dev
ENV GO111MODULE=on
RUN go install github.com/cespare/reflex@latest

COPY go.mod .
COPY go.sum .

RUN go mod download

COPY . .

RUN go build -o ./run .

FROM alpine:lastest
RUN apk --no-cache ca-certificates
WORKDIR /root/

# Copy executable from builder
COPY --from=builder /go/src/app/run .

EXPOSE 8080
CMD ["./run"]