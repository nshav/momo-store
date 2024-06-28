# Frontend dockerfile momo-store

# Build frontend
FROM node:16.20.0-alpine3.18 as builder
# Add frontend version
ARG VERSION=${VERSION}
WORKDIR /app
# Copy source files
COPY . .
# Build source
RUN npm install && NODE_ENV=production npm run build

# Run frontend
FROM nginx:stable-alpine
# Add frontend version
ARG VERSION=${VERSION}
# Copy conf files from builder
COPY --from=builder /app/dist /usr/share/nginx/html
#COPY --from=builder /app/default.conf /etc/nginx/conf.d/default.conf
EXPOSE 8080
