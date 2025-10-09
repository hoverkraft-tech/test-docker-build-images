FROM scratch AS base

USER test

FROM nginx:1-alpine AS prod

HEALTHCHECK --interval=5s --timeout=3s --retries=3 CMD ["curl", "-f", "http://localhost:8080/health/check"]

# Configure nginx to listen on port 8080
RUN sed -i 's/listen       80;/listen       8080;/' /etc/nginx/conf.d/default.conf

# Create a hmtl page for healthcheck
RUN mkdir -p /usr/share/nginx/html/health/check && echo "<html><body><h1>OK</h1></body></html>" > /usr/share/nginx/html/health/check/index.html

ARG BUILD_RUN_ID
RUN test -n "$BUILD_RUN_ID" || (echo "Error: BUILD_RUN_ID is not set" && exit 1);

EXPOSE 8080