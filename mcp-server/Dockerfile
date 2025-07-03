FROM node:23.11.0-bookworm AS builder

ARG BITBUCKET_MCP_SERVER_VERSION=v1.41.1

RUN apt-get update && apt-get install -y git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Set the working directory
WORKDIR /usr/src/app

RUN git clone --branch ${BITBUCKET_MCP_SERVER_VERSION} --single-branch --depth 1 https://github.com/aashari/mcp-server-atlassian-bitbucket.git .

# Install dependencies without running prepare scripts
RUN npm install --ignore-scripts

# Build the TypeScript code
RUN npm run build

# Ensure the entrypoint is executable (already set in prepare, but reensure here)
RUN chmod +x dist/index.js

FROM node:23.11.0-bookworm AS final

WORKDIR /usr/src/app
COPY --from=builder /usr/src/app/dist ./dist
COPY --from=builder /usr/src/app/node_modules ./node_modules

CMD ["node", "dist/index.js"]

EXPOSE 3000
