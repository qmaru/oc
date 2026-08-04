FROM alpine:3 AS extension

RUN apk add --no-cache curl upx

RUN curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh

RUN if [ "${TARGETPLATFORM}" != "linux/arm64" ]; then \
      upx --best --lzma /root/.local/bin/rtk; \
    fi

FROM node:24-alpine

LABEL org.opencontainers.image.title="opencode-node"
LABEL org.opencontainers.image.description="Node 24 image for opencode agents"

WORKDIR /workspace

RUN apk add --no-cache ca-certificates tzdata libstdc++ fontconfig

COPY --from=ghcr.io/anomalyco/opencode:latest /usr/local/bin/opencode /usr/local/bin/
COPY --from=extension /root/.local/bin/rtk /usr/local/bin/rtk

COPY AGENTS.md opencode.json /workspace/
COPY oc-node/README.md /workspace/README.md
COPY oc-node/.agents /workspace/.agents

RUN rtk init -g --opencode

ENV TZ=UTC \
    NODE_ENV=1

ENTRYPOINT ["opencode"]
