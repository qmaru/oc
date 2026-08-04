FROM alpine:3 AS extension

RUN apk add --no-cache curl upx

RUN curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh

RUN if [ "$TARGETARCH" != "arm64" ]; then \
      upx --best --lzma /root/.local/bin/rtk; \
    fi

FROM ghcr.io/anomalyco/opencode:latest

LABEL org.opencontainers.image.title="opencode-base"
LABEL org.opencontainers.image.description="Busybox image for opencode agents"

USER root

RUN apk add --no-cache curl jq ca-certificates tzdata fontconfig

COPY --from=extension /root/.local/bin/rtk /usr/local/bin/rtk

COPY AGENTS.md opencode.json /workspace/
COPY oc-base/README.md /workspace/README.md
COPY oc-base/.agents /workspace/.agents

RUN rtk init -g --opencode

ENV TZ=UTC

WORKDIR /workspace
