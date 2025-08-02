# Dockerfile Documentation

## Overview

This document provides an explanation of the purpose and functionality of the `NPX-tool-Dockerfile` and `UV-tool-Dockerfile`. Both Dockerfiles are used to build container images for the [mcp-proxy](https://github.com/sparfenyuk/mcp-proxy) tool, which facilitates server transport switching. Each Dockerfile has specific configurations and dependencies tailored to its use case.

---

## `NPX-tool-Dockerfile`

### Purpose
The `NPX-tool-Dockerfile` is designed to build a container image for `mcp-proxy` with Node.js and `npx` installed. This setup is useful for scenarios where Node.js-based tools or scripts are required alongside the `mcp-proxy` functionality.

### Key Features
1. **Base Image**: Uses `ghcr.io/sparfenyuk/mcp-proxy:{MCP-PROXY-VERSION}` as the base image.
2. **Pip Configuration**: Configures `pip` to use the Tsinghua mirror for faster Python package installations in China.
3. **Node.js and npx Installation**: Installs Node.js and `npx` for executing Node.js-based tools.
4. **Exposed Port**: Exposes port `8080` for the `mcp-proxy` server.
5. **Entrypoint**: Sets `mcp-proxy` as the default entrypoint.

You can update these features based on your specific requirements.

### Example Build and Run Commands

You can build the source code using the `npx` tool, which is a package runner tool that comes with Node.js. It allows you to run Node.js packages without installing them globally.
```bash
# Build the Docker image
docker build -t <your-registry>/mcp-proxy-npx-tool:latest -f NPX-tool-Dockerfile .

# You can refer to the `examples/mcp-servers-config` directory for example server configuration files.
docker run -v <local-path>:/app/mcp-servers-config/ -p 8080:8080 <your-registry>/mcp-proxy-npx-tool:latest --port=8080 --host=0.0.0.0 --named-server-config /app/mcp-servers-config/mcp-server-time.json
```

Or you can download the docker image directly from the registry and then run it:
```bash
docker pull xuerongjing/mcp-proxy-npx-tool:latest

docker run -v <local-path>:/app/mcp-servers-config/ -p 8080:8080 xuerongjing/mcp-proxy-npx-tool:latest --port=8080 --host=0.0.0.0 --named-server-config /app/mcp-servers-config/mcp-server-time.json
```

---

## `UV-tool-Dockerfile`

### Purpose
The `UV-tool-Dockerfile` is designed to build a container image for `mcp-proxy` with the `uv` Python package installed. This setup is optimized for Python-based workflows and dependency management using `uv`.

### Key Features
1. **Base Image**: Uses `ghcr.io/sparfenyuk/mcp-proxy:{MCP-PROXY-VERSION}` as the base image.
2. **Pip Configuration**: Configures `pip` to use the Tsinghua mirror for faster Python package installations in China.
3. **UV Configuration**: Configures `uv` to use the Tsinghua mirror and installs the `uv` package.
4. **Exposed Port**: Exposes port `8080` for the `mcp-proxy` server.
5. **Entrypoint**: Sets `mcp-proxy` as the default entrypoint.

You can update these features based on your specific requirements.

### Example Build and Run Commands

You can build the source code using the `uv` tool, which is a Python package manager that simplifies dependency management and installation.
```bash
# Build the Docker image
docker build -t <your-registry>/mcp-proxy-uv-tool:latest -f UV-tool-Dockerfile .

# You can refer to the `examples/mcp-servers-config` directory for example server configuration files.
docker run -v <local-path>:/app/mcp-servers-config/ -p 8080:8080 <your-registry>/mcp-proxy-uv-tool:latest --port=8080 --host=0.0.0.0 --named-server-config /app/mcp-servers-config/mcp-server-sequential-thinking.json
```

Or you can download the docker image directly from the registry and then run it:
```bash
docker pull xuerongjing/mcp-proxy-uv-tool:latest

docker run -v <local-path>:/app/mcp-servers-config/ -p 8080:8080 xuerongjing/mcp-proxy-uv-tool:latest --port=8080 --host=0.0.0.0 --named-server-config /app/mcp-servers-config/mcp-server-sequential-thinking.json
```

---

## Notes
- Replace `<your-registry>` with your container registry URL.
- Replace `<local-path>` with the local directory path containing the server configuration files.
- Both Dockerfiles are optimized for specific use cases. Choose the appropriate one based on your project requirements.