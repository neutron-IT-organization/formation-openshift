# Use the Red Hat Universal Base Image (UBI) as the base image
FROM registry.access.redhat.com/ubi8/go-toolset

# Set the working directory inside the container
#WORKDIR /go/src/app

# Copy the local package files to the container's workspace
COPY . .

# Build the Go application
RUN go build main.go

# Command to run the application
CMD ["./main"]
