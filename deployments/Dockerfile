FROM golang:1.22-alpine AS builder

RUN apk add --no-cache make

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY cmd ./cmd
COPY internal ./internal
COPY configs ./configs
COPY reports ./reports
COPY Makefile ./

RUN make build

FROM alpine:latest

COPY --from=builder /app/server ./
COPY --from=builder /app/configs/config.json ./configs/

CMD ["./server", "configs/config.json"]
