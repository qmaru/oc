FROM cgr.dev/chainguard/wolfi-base AS build

RUN apk add --no-cache curl bash

# opencode core
RUN curl -fsSL https://opencode.ai/v2/install | bash

FROM cgr.dev/chainguard/wolfi-base AS runtime

WORKDIR /workspace

ENV TZ=UTC

RUN apk add --no-cache curl jq bash fd ripgrep ca-certificates tzdata fontconfig

COPY --from=build /root/.opencode/bin/opencode /usr/local/bin/opencode

COPY AGENTS.md opencode.json ./

FROM runtime

LABEL org.opencontainers.image.title="opencode-node"
LABEL org.opencontainers.image.description="Node 24 image for opencode agents"

RUN apk add --no-cache nodejs-24-minimal npm-12

COPY oc-node/README.md README.md
COPY oc-node/.agents .agents

ENV TZ=UTC \
    LANG=C.UTF-8 \
    LC_ALL=C.UTF-8 \
    NODE_ENV=production \
    NPM_CONFIG_UPDATE_NOTIFIER=false \
    NPM_CONFIG_FUND=false

ENTRYPOINT ["opencode"]
