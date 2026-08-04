FROM cgr.dev/chainguard/wolfi-base AS base

RUN apk add --no-cache curl bash

RUN curl -fsSL https://opencode.ai/install | bash

RUN curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh

FROM cgr.dev/chainguard/wolfi-base

LABEL org.opencontainers.image.title="opencode-base"
LABEL org.opencontainers.image.description="Busybox image for opencode agents"

WORKDIR /workspace

RUN apk add --no-cache ca-certificates tzdata fontconfig curl jq

COPY --from=base /root/.opencode/bin/opencode /usr/local/bin/opencode
COPY --from=base /root/.local/bin/rtk /usr/local/bin/rtk

COPY AGENTS.md opencode.json /workspace/
COPY oc-base/README.md /workspace/README.md
COPY oc-base/.agents /workspace/.agents

ENV TZ=UTC

ENTRYPOINT ["opencode"]
