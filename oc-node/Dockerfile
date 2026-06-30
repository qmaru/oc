FROM node:24-alpine

WORKDIR /workspace

RUN apk add --no-cache ca-certificates tzdata libstdc++

COPY --from=ghcr.io/anomalyco/opencode:latest /usr/local/bin/opencode /usr/local/bin/

COPY AGENTS.md opencode.json /workspace/
COPY oc-node/README.md /workspace/README.md
COPY oc-node/.agents /workspace/.agents

ENV TZ=UTC

ENV NODE_ENV=production

ENTRYPOINT ["opencode"]