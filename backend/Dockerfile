# Backend dockerfile momo-store

# Build backend
FROM golang:1.22.1-alpine AS builder
# Add backend version
#ARG VERSION=${VERSION}
# Copy source filesi
WORKDIR /app
COPY . .
# Install dependences and start building backend
RUN go mod download && go build -o /momo-backend ./cmd/api

# Run backend
FROM alpine:3.19.1
# Add backend version
#ARG VERSION=${VERSION}
WORKDIR /app
RUN apk --no-cache add curl
# Copy results file from builder
COPY --from=builder momo-backend /app/momo-backend
EXPOSE 8081
# Start app backend
ENTRYPOINT ["/app/momo-backend"]

