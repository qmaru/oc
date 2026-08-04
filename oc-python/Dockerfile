FROM python:3.13-alpine

LABEL org.opencontainers.image.title="opencode-python"
LABEL org.opencontainers.image.description="Python 3.13 image for opencode agents"

WORKDIR /workspace

RUN apk add --no-cache ca-certificates tzdata libstdc++ fontconfig

COPY --from=ghcr.io/anomalyco/opencode:latest /usr/local/bin/opencode /usr/local/bin/

COPY AGENTS.md opencode.json /workspace/
COPY oc-python/README.md /workspace/README.md
COPY oc-python/.agents /workspace/.agents

ENV TZ=UTC \
    PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

ENTRYPOINT ["opencode"]
