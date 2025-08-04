# GCP Diagram MCP Server

Model Context Protocol (MCP) server for GCP Diagrams

This MCP server that seamlessly creates [diagrams](https://diagrams.mingrammer.com/) using the Python diagrams package DSL. This server allows you to generate GCP diagrams, sequence diagrams, flow diagrams, and class diagrams using Python code.

[![Tests](https://img.shields.io/badge/tests-passing-brightgreen.svg)](https://github.com/gcplabs/mcp/blob/main/src/gcp-diagram-mcp-server/tests/)

## Prerequisites

1. Install `uv` from [Astral](https://docs.astral.sh/uv/getting-started/installation/) or the [GitHub README](https://github.com/astral-sh/uv#installation)
2. Install Python using `uv python install 3.10`
3. Install GraphViz https://www.graphviz.org/

## Installation
Configure the MCP server in your MCP client configuration (e.g., for Google Cloud CLI, edit `~/.gemini/settings.json`):

```json
{
  "theme": "Default Light",
  "selectedAuthType": "gemini-api-key",
  "mcpServers": {
    "gcplabs.gcp-diagram-mcp-server": {
      "command": "uvx",
      "args": [
        "--from",
        "gcplabs.gcp-diagram-mcp-server@git+https://github.com/shawnho1018/gcp-diagram-mcp-server.git",
        "gcplabs.gcp-diagram-mcp-server"
      ],
      "env": {
        "FASTMCP_LOG_LEVEL": "ERROR"
      },
      "autoApprove": [],
      "disabled": false
    }
  }
}
```

## Features

The Diagrams MCP Server provides the following capabilities:

1. **Generate Diagrams**: Create professional diagrams using Python code
2. **Multiple Diagram Types**: Support for GCP architecture, sequence diagrams, flow charts, class diagrams, and more
3. **Customization**: Customize diagram appearance, layout, and styling
4. **Security**: Code scanning to ensure secure diagram generation

## Quick Example
Try to input the following questions after you start gemini-cli
1. Generate a GCP diagram which uses all tf files in @iac/ and save the diagram as iac.png
2. Generate a GCP diagram which uses all yaml files in @kubernetes-manifests/ and save the diagram as k8s.png

The process is produced the python diagram code in the following format to generate the graph.
```python
from diagrams import Diagram
from diagrams.gcp.compute import GCE
from diagrams.gcp.database import SQL
from diagrams.gcp.network import LoadBalancing

with Diagram("Web Service", show=False):
    lb = LoadBalancing("lb")
    web = GCE("web")
    db = SQL("userdb")

    lb >> web >> db
```
