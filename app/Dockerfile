# Updating my dockerfile butI will still be using the Nginx alpine image as the base image

# Use minimal and secure nginx base image
FROM nginx:alpine:3.18

# Set working directory inside container
WORKDIR /usr/share/nginx/html

# Copyin only necessary app files
COPY . .

# Change file ownership to nginx user for safety
RUN chown -R nginx:nginx /usr/share/nginx/html

# Drop privileges to non-root
USER nginx

# Expose nginx default port
EXPOSE 80

# Ensure package database fresh and upgrade pcre2 to fixed version, added for trivy scan.
RUN apk update && \
    apk add --no-cache pcre2=10.46-r0

# Optional: Health check for container monitoring
HEALTHCHECK CMD wget -q --spider http://localhost:80 || exit 1
