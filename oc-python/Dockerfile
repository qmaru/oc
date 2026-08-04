FROM cgr.dev/chainguard/wolfi-base AS base

RUN apk add --no-cache curl bash

RUN curl -fsSL https://opencode.ai/install | bash

RUN curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh

FROM cgr.dev/chainguard/wolfi-base

FROM cgr.dev/chainguard/wolfi-base

LABEL org.opencontainers.image.title="opencode-python"
LABEL org.opencontainers.image.description="Python 3.13 image for opencode agents"

WORKDIR /workspace

RUN apk add --no-cache ca-certificates tzdata fontconfig python-3.13-base py3.13-pip-base

COPY --from=base /root/.opencode/bin/opencode /usr/local/bin/opencode
COPY --from=base /root/.local/bin/rtk /usr/local/bin/rtk

COPY AGENTS.md opencode.json /workspace/
COPY oc-python/README.md /workspace/README.md
COPY oc-python/.agents /workspace/.agents

RUN ln -s /usr/bin/python3.13 /usr/bin/python \
    && ln -s /usr/bin/pip3.13 /usr/bin/pip

ENV TZ=UTC \
    PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

ENTRYPOINT ["opencode"]
