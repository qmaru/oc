FROM ghcr.io/anomalyco/opencode:latest

USER root

RUN apk add --no-cache curl jq ca-certificates

COPY AGENTS.md opencode.json /workspace/
COPY oc-base/.agents /workspace/.agents

WORKDIR /workspace
