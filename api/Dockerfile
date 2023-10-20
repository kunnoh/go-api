FROM --platform=$BUILDPLATFORM golang:1.18-alpine AS builder

WORKDIR /api

ENV CGO_ENABLED 0
ENV GOPATH /go
ENV GOCACHE /go-build

COPY go.mod go.sum ./
RUN --mount=type=cache,target=/go/pkg/mod/cache \
    go mod download

COPY . .

RUN --mount=type=cache,target=/go/pkg/mod/cache \
    --mount=type=cache,target=/go-build \
    go build -o bin/backend-api main.go

CMD ["/api/bin/backend-api"]

FROM builder as dev-envs

RUN apk update

RUN <<EOF
addgroup -S docker
adduser -S --shell /bin/bash --ingroup docker
EOF

# install Docker tools (cli, buildx, compose)
COPY --from=gloursdocker/docker / /

CMD ["go", "run", "main.go"]

FROM scratch
COPY --from=builder /api/bin/backend-api /usr/local/bin/backend-api
CMD ["/usr/local/bin/backend-api"]
