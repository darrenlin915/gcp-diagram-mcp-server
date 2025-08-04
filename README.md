# GCP Diagram MCP Server

Model Context Protocol (MCP) server for GCP Diagrams

This MCP server that seamlessly creates [diagrams](https://diagrams.mingrammer.com/) using the Python diagrams package DSL. This server allows you to generate GCP diagrams, sequence diagrams, flow diagrams, and class diagrams using Python code.

[![Tests](https://img.shields.io/badge/tests-passing-brightgreen.svg)](https://github.com/gcplabs/mcp/blob/main/src/gcp-diagram-mcp-server/tests/)

## Prerequisites

1. Install `uv` from [Astral](https://docs.astral.sh/uv/getting-started/installation/) or the [GitHub README](https://github.com/astral-sh/uv#installation)
2. Install Python using `uv python install 3.10`
3. Install GraphViz https://www.graphviz.org/

## Installation
| [![Install MCP Server](https://cursor.com/deeplink/mcp-install-light.svg)](https://cursor.com/install-mcp?name=gcplabs.gcp-diagram-mcp-server&config=eyJjb21tYW5kIjoidXZ4IGdjcGxhYnMuZ2NwLWRpYWdyYW0tbWNwLXNlcnZlciIsImVudiI6eyJGQVNUTUNQX0xPR19MRVZFTCI6IkVSUk9SIn0sImF1dG9BcHByb3ZlIjpbXSwiZGlzYWJsZWQiOmZhbHNlfQ%3D%3D) | [![Install on VS Code](https://img.shields.io/badge/Install_on-VS_Code-4285F4?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=GCP%20Diagram%20MCP%20Server&config=%7B%22command%22%3A%22uvx%22%2C%22args%22%3A%5B%22gcplabs.gcp-diagram-mcp-server%22%5D%2C%22env%22%3A%7B%22FASTMCP_LOG_LEVEL%22%3A%22ERROR%22%7D%2C%22autoApprove%22%3A%5B%5D%2C%22disabled%22%3Afalse%7D) |

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