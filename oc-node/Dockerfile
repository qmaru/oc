FROM cgr.dev/chainguard/wolfi-base AS base

RUN apk add --no-cache curl bash

RUN curl -fsSL https://opencode.ai/install | bash

RUN curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh

FROM cgr.dev/chainguard/wolfi-base

LABEL org.opencontainers.image.title="opencode-node"
LABEL org.opencontainers.image.description="Node 24 image for opencode agents"

WORKDIR /workspace

RUN apk add --no-cache ca-certificates tzdata fontconfig nodejs-24-minimal npm-12

COPY --from=base /root/.opencode/bin/opencode /usr/local/bin/opencode
COPY --from=base /root/.local/bin/rtk /usr/local/bin/rtk

COPY AGENTS.md opencode.json /workspace/
COPY oc-node/README.md /workspace/README.md
COPY oc-node/.agents /workspace/.agents

ENV TZ=UTC \
    NODE_ENV=1

ENTRYPOINT ["opencode"]
