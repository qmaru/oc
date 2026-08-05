FROM cgr.dev/chainguard/wolfi-base AS build

RUN apk add --no-cache curl bash

# opencode core
RUN curl -fsSL https://opencode.ai/install | bash

# helper tools
RUN curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh

FROM cgr.dev/chainguard/wolfi-base AS runtime

WORKDIR /workspace

ENV TZ=UTC

RUN apk add --no-cache ca-certificates tzdata fontconfig

COPY --from=build /root/.opencode/bin/opencode /usr/local/bin/opencode
COPY --from=build /root/.local/bin/rtk /usr/local/bin/rtk

COPY AGENTS.md opencode.json ./

FROM runtime

LABEL org.opencontainers.image.title="opencode-node"
LABEL org.opencontainers.image.description="Node 24 image for opencode agents"

RUN apk add --no-cache nodejs-24-minimal npm-12

COPY oc-node/README.md README.md
COPY oc-node/.agents .agents

ENV NODE_ENV=production \
    NPM_CONFIG_UPDATE_NOTIFIER=false \
    NPM_CONFIG_FUND=false

ENTRYPOINT ["opencode"]
