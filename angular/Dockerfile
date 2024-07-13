FROM node:20-buster-slim

RUN apt-get update -qq && apt-get install -qq -y --no-install-recommends \
  curl ca-certificates \
  && rm -rf /var/lib/apt/lists/*

ENV NPM_CONFIG_LOGLEVEL=warn
ENV NG_CLI_ANALYTICS=false

RUN npm install -g @angular/cli@^18.0.0

RUN arch=$(uname -m) && \
  if [ "${arch}" = "aarch64" ]; then \
  arch="arm64"; \
  fi && \
  curl -fsSL "https://github.com/a8m/envsubst/releases/download/v1.4.2/envsubst-Linux-${arch}" -o /usr/local/bin/envsubst && chmod +x /usr/local/bin/envsubst

WORKDIR /src
COPY --chown=root:root template /template
COPY --chown=root:root generate /generate

CMD [ "/generate" ]