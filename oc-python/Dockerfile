FROM python:3.13-alpine

WORKDIR /workspace

RUN apk add --no-cache ca-certificates libstdc++

COPY --from=ghcr.io/anomalyco/opencode:latest /usr/local/bin/opencode /usr/local/bin/

COPY AGENTS.md opencode.json /workspace/
COPY oc-python/.agents /workspace/.agents

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

ENTRYPOINT ["opencode"]
