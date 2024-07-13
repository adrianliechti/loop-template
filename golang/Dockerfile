FROM golang:1-alpine

RUN apk add --no-cache ca-certificates bash curl

RUN arch=$(uname -m) && \
    if [ "${arch}" = "aarch64" ]; then \
    arch="arm64"; \
    fi && \
    curl -fsSL "https://github.com/a8m/envsubst/releases/download/v1.4.2/envsubst-Linux-${arch}" -o /usr/local/bin/envsubst && chmod +x /usr/local/bin/envsubst

WORKDIR /src
COPY --chown=root:root app /app
COPY --chown=root:root template /template
COPY --chown=root:root generate /generate

CMD [ "/generate" ]