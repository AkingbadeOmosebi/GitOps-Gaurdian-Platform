# Updating my dockerfile butI will still be using the Nginx alpine image as the base image

# Use minimal and secure nginx base image
FROM nginx:1.25.2-alpine

# Set working directory inside container
WORKDIR /usr/share/nginx/html

# Copyin only necessary app files
COPY . .

# Install packages for Trivy as root (before switching user)
RUN apk update && \
    apk add --no-cache pcre2 wget && \
    rm -rf /var/cache/apk/*

# Change file ownership to nginx user for safety
RUN chown -R nginx:nginx /usr/share/nginx/html

# Drop privileges to non-root
USER nginx

# Expose nginx default port
EXPOSE 80

# Optional: Health check for container monitoring
HEALTHCHECK CMD wget -q --spider http://localhost:80 || exit 1
