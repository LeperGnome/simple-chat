FROM golang:1.22.3-alpine as DependenciesInstalled

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

FROM golang:1.22.3-alpine as AirInstalled

RUN go install github.com/air-verse/air@latest

FROM golang:1.22.3-alpine

COPY --from=DependenciesInstalled /go/pkg/mod /go/pkg/mod
COPY --from=AirInstalled /go/bin/air /go/bin/air

WORKDIR /app

COPY . .

CMD ["air", "-c", "./build/dev/auth/.air.toml"]
