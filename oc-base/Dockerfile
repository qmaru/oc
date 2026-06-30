FROM ghcr.io/anomalyco/opencode:latest

USER root

RUN apk add --no-cache curl jq ca-certificates tzdata

COPY AGENTS.md opencode.json /workspace/
COPY oc-base/README.md /workspace/README.md
COPY oc-base/.agents /workspace/.agents

ENV TZ=UTC

WORKDIR /workspace
