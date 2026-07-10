FROM golang:1.22-alpine AS builder

WORKDIR /app

# Install git (needed for some Go modules)


# Cache dependencies
COPY go.mod go.sum ./
RUN go mod download

# Copy source code
COPY . .

# Build static binary
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o devboard-backend .


# -------- Stage 2: Runtime --------
FROM alpine:3.20

WORKDIR /app

# Create non-root user
RUN adduser -D -u 10001 app

# Copy only the binary from builder
COPY --from=builder /app/devboard-backend .

# Set permissions
RUN chown app:app /app
USER app

EXPOSE 8080

ENTRYPOINT ["./devboard-backend"]
