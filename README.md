# oc

An agent framework built on top of opencode.

## Constraints

* `AGENTS.md`: Skill-only task execution.
* `opencode.json`: Default model and policies.

## .agents

Skills and tools configuration.

## oc-base

Minimal runtime environment.

+ curl
+ jq

```sh
cd oc-base
docker compose build
# prefix
IMAGE_PREFIX="ghcr.io/[namespace]" docker compose build
```

## oc-python

Python runtime environment.

```sh
cd oc-python
docker compose build
```

## oc-node

Node.js runtime environment.

```sh
cd oc-node
docker compose build
```
