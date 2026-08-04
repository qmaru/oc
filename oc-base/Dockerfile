FROM ghcr.io/anomalyco/opencode:latest

LABEL org.opencontainers.image.title="opencode-base"
LABEL org.opencontainers.image.description="Busybox image for opencode agents"

USER root

RUN apk add --no-cache curl jq ca-certificates tzdata fontconfig

COPY AGENTS.md opencode.json /workspace/
COPY oc-base/README.md /workspace/README.md
COPY oc-base/.agents /workspace/.agents

ENV TZ=UTC

WORKDIR /workspace

ENTRYPOINT ["opencode"]
