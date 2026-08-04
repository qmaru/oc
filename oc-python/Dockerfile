FROM alpine:3 AS extension

RUN apk add --no-cache curl upx

RUN curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh

RUN if [ "$TARGETARCH" != "arm64" ]; then \
      upx --best --lzma /root/.local/bin/rtk; \
    fi

FROM python:3.13-alpine

LABEL org.opencontainers.image.title="opencode-python"
LABEL org.opencontainers.image.description="Python 3.13 image for opencode agents"

WORKDIR /workspace

RUN apk add --no-cache ca-certificates tzdata libstdc++ fontconfig

COPY --from=ghcr.io/anomalyco/opencode:latest /usr/local/bin/opencode /usr/local/bin/
COPY --from=extension /root/.local/bin/rtk /usr/local/bin/rtk

COPY AGENTS.md opencode.json /workspace/
COPY oc-python/README.md /workspace/README.md
COPY oc-python/.agents /workspace/.agents

RUN rtk init -g --opencode

ENV TZ=UTC \
    PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

ENTRYPOINT ["opencode"]
