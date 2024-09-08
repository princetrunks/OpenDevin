---
sidebar_position: 2
---

# Getting Started

## System Requirements

* Docker version 26.0.0+ or Docker Desktop 4.31.0+
* You must be using Linux or Mac OS
  * If you are on Windows, you must use [WSL](https://learn.microsoft.com/en-us/windows/wsl/install)

## Installation

The easiest way to run OpenHands is in Docker. You can change `WORKSPACE_BASE` below to point OpenHands to
existing code that you'd like to modify.

```bash
export WORKSPACE_BASE=$(pwd)/workspace

docker run -it --pull=always \
    -e SANDBOX_RUNTIME_CONTAINER_IMAGE=ghcr.io/all-hands-ai/runtime:0.9.2-nikolaik \
    -e SANDBOX_USER_ID=$(id -u) \
    -e WORKSPACE_MOUNT_PATH=$WORKSPACE_BASE \
    -v $WORKSPACE_BASE:/opt/workspace_base \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -p 3000:3000 \
    --add-host host.docker.internal:host-gateway \
    --name openhands-app-$(date +%Y%m%d%H%M%S) \
    ghcr.io/all-hands-ai/openhands:0.9
```

You can also run OpenHands in a scriptable [headless mode](https://docs.all-hands.dev/modules/usage/how-to/headless-mode),
or as an [interactive CLI](https://docs.all-hands.dev/modules/usage/how-to/cli-mode).

## Setup

After running the command above, you'll find OpenHands running at [http://localhost:3000](http://localhost:3000).

The agent will have access to the `./workspace` folder to do its work. You can copy existing code here, or change `WORKSPACE_BASE` in the
command to point to an existing folder.

Upon launching OpenHands, you'll see a settings modal. You must select an LLM backend using `Model`, and enter a corresponding `API Key`.
These can be changed at any time by selecting the `Settings` button (gear icon) in the UI.
If the required `Model` does not exist in the list, you can toggle `Use custom model` and manually enter it in the text box.

<img src="/img/settings-screenshot.png" alt="settings-modal" width="340" />

## Versions

The command above pulls the `0.9` tag, which represents the most recent stable release of OpenHands. You have other options as well:
- For a specific release, use `ghcr.io/all-hands-ai/openhands:$VERSION`, replacing $VERSION with the version number.
- We use semver, and release major, minor, and patch tags. So `0.9` will automatically point to the latest `0.9.x` release, and `0` will point to the latest `0.x.x` release.
- For the most up-to-date development version, you can use `ghcr.io/all-hands-ai/openhands:main`. This version is unstable and is recommended for testing or development purposes only.

You can choose the tag that best suits your needs based on stability requirements and desired features.

For the development workflow, see [Development.md](https://github.com/All-Hands-AI/OpenHands/blob/main/Development.md).

Are you having trouble? Check out our [Troubleshooting Guide](https://docs.all-hands.dev/modules/usage/troubleshooting).