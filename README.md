# APISIX MCP Bridge Plugin Example

This repository demonstrates how to use the APISIX MCP Bridge plugin to integrate Model Context Protocol (MCP) servers with APISIX. The setup includes building a custom APISIX Docker image with Docker client capabilities and creating a Bitbucket MCP server that communicates via stdio.

## Overview

The MCP Bridge plugin allows APISIX to act as a proxy for MCP servers, enabling seamless integration between MCP clients (like VS Code) and MCP servers through HTTP/SSE endpoints.

### Components

- **Custom APISIX Image**: Enhanced with Docker client for running containerized MCP servers
- **Bitbucket MCP Server**: Containerized MCP server for Atlassian Bitbucket integration
- **MCP Bridge Plugin**: APISIX plugin that bridges HTTP/SSE to stdio MCP communication

## Prerequisites

- Docker and Docker Compose
- VS Code with MCP extension (for client testing)
- Atlassian Bitbucket credentials (username and app password)

## Configuration

### Environment Variables

Edit `.env` with your Bitbucket credentials:

```properties
ATLASSIAN_SITE_NAME="https://api.bitbucket.org"
ATLASSIAN_BITBUCKET_USERNAME="your_username"
ATLASSIAN_BITBUCKET_APP_PASSWORD="your_app_password"
```

## Building Images

### Build APISIX Image

The custom APISIX image includes Docker client for running containerized MCP servers:

```bash
docker-compose build apisix
```

### Build Bitbucket MCP Server Image

```bash
docker-compose build mcp-bitbucket
```

### Build All Images with Docker Compose

```bash
docker-compose build
```

## Running the Server

### Start All Services

```bash
docker-compose up -d
```

This will start:
- APISIX on port 80 with MCP Bridge plugin
- Whoami service for testing

### Verify Services

Check that APISIX is running:

```bash
curl http://localhost/whoami
```

Test MCP Bridge endpoint:

```bash
curl http://localhost/mcp-bitbucket/
```

## VS Code MCP Client Configuration

### Using Server-Sent Events (SSE)

Configure VS Code MCP client to connect to the APISIX MCP Bridge endpoint:

1. Install the MCP extension in VS Code
2. Add the following configuration to your VS Code settings or MCP client config:

```json
{
  "servers": {
    "mcp-bitbucket": {
      "type": "sse",
      "url": "http://localhost/mcp-bitbucket"
    }
  }
}
```

## Cleanup

Stop and remove all services:

```bash
docker-compose down
```

Remove built images:

```bash
docker rmi arulrajnet/apisix:dev arulrajnet/mcp-bitbucket:v1.39.7
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Author

<p align="center">
  <a href="https://x.com/arulrajnet">
    <img src="https://github.com/arulrajnet.png?size=100" alt="Arulraj V" width="100" height="100" style="border-radius: 50%;" class="avatar-user">
  </a>
  <br>
  <strong>Arul</strong>
  <br>
  <a href="https://x.com/arulrajnet">
    <img src="https://img.shields.io/badge/Follow-%40arulrajnet-1DA1F2?style=for-the-badge&logo=x&logoColor=white" alt="Follow @arulrajnet on X">
  </a>
  <a href="https://github.com/arulrajnet">
    <img src="https://img.shields.io/badge/GitHub-arulrajnet-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub @arulrajnet">
  </a>
  <a href="https://linkedin.com/in/arulrajnet">
    <img src="https://custom-icon-badges.demolab.com/badge/LinkedIn-arulrajnet-0A66C2?style=for-the-badge&logo=linkedin-white&logoColor=white" alt="LinkedIn @arulrajnet">
  </a>
</p>
