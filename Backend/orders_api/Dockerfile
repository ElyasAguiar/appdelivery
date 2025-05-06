FROM golang:1.23-alpine AS builder
# Set the working directory inside the container
WORKDIR /usr/src/app

COPY ./Backend/orders_api/go.mod ./Backend/orders_api/go.sum ./
RUN go mod download && go mod verify

COPY ./Backend/orders_api/ .
RUN go build -v -o /usr/local/bin/app

FROM scratch
WORKDIR /usr/src/app
COPY ./Backend/orders_api/.env .env
COPY --from=builder /usr/local/bin/app .
CMD [ "./app" ]
