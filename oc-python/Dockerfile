FROM cgr.dev/chainguard/wolfi-base AS build

RUN apk add --no-cache curl bash

# opencode core
RUN curl -fsSL https://opencode.ai/install | bash

# helper tools
RUN curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh

FROM cgr.dev/chainguard/wolfi-base AS runtime

WORKDIR /workspace

ENV TZ=UTC

RUN apk add --no-cache ca-certificates tzdata fontconfig

COPY --from=build /root/.opencode/bin/opencode /usr/local/bin/opencode
COPY --from=build /root/.local/bin/rtk /usr/local/bin/rtk

COPY AGENTS.md opencode.json ./

FROM runtime

LABEL org.opencontainers.image.title="opencode-python"
LABEL org.opencontainers.image.description="Python 3.13 image for opencode agents"

RUN apk add --no-cache python-3.13-base py3.13-pip-base

COPY oc-python/README.md README.md
COPY oc-python/.agents .agents

RUN ln -sf /usr/bin/python3.13 /usr/bin/python \
    && ln -sf /usr/bin/pip3.13 /usr/bin/pip

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PIP_DISABLE_PIP_VERSION_CHECK=1

ENTRYPOINT ["opencode"]
