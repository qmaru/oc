FROM cgr.dev/chainguard/wolfi-base AS build

RUN apk add --no-cache curl bash

# opencode core
RUN curl -fsSL https://opencode.ai/install | bash

# helper tools
RUN curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh

FROM cgr.dev/chainguard/wolfi-base AS runtime

WORKDIR /workspace

ENV TZ=UTC \
    LANG=C.UTF-8 \
    LC_ALL=C.UTF-8

RUN apk add --no-cache ca-certificates tzdata fontconfig

COPY --from=build /root/.opencode/bin/opencode /usr/local/bin/opencode
COPY --from=build /root/.local/bin/rtk /usr/local/bin/rtk

COPY AGENTS.md opencode.json ./

FROM runtime

LABEL org.opencontainers.image.title="opencode-base"
LABEL org.opencontainers.image.description="Busybox image for opencode agents"

RUN apk add --no-cache curl jq

COPY oc-base/README.md README.md
COPY oc-base/.agents .agents

ENTRYPOINT ["opencode"]
