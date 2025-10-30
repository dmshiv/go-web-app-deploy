#multistage docker file 
# Stage 1: Build the Go application
FROM golang:1.22-alpine as base

WORKDIR /app

##go.mod has all the dependencies 
COPY go.mod .  
RUN go mod download

COPY . .

RUN go build -o main .

# ##u can finish the docker file here itself
# ##but it wont reduce secure ot reduce the image size

# EXPOSE 8080

# CMD ["./main"]


# Stage 2: distroless image

FROM gcr.io/distroless/base

##from above stage copy the built binary

COPY --from=base /app/main .

##copy static files too
COPY --from=base /app/static ./static

EXPOSE 8080
CMD ["./main"]
