# Awesome MCP

> A comprehensive curated list of Model Context Protocol (MCP) resources, servers, clients, frameworks, and tools.

[![Stars](https://img.shields.io/github/stars/vivy-yi/awesome-mcp)](https://github.com/vivy-yi/awesome-mcp)
[![License](https://img.shields.io/badge/license-CC0--1.0-blue)](LICENSE)

Model Context Protocol (MCP) is an open protocol that enables AI assistants to connect with external data sources and tools. This list aggregates MCP resources from across the ecosystem.

## Featured - Top 15 Popular MCP Servers

The most popular and widely-used MCP servers in the ecosystem:

| # | Project | Stars | Description |
|---|---------|-------|-------------|
| 1 | [github/github-mcp-server](https://github.com/github/github-mcp-server) | ![Stars](https://img.shields.io/github/stars/github/github-mcp-server) | GitHub's official MCP server - Issues, PRs, repos |
| 2 | [microsoft/playwright-mcp](https://github.com/microsoft/playwright-mcp) | ![Stars](https://img.shields.io/github/stars/microsoft/playwright-mcp) | Browser automation with Playwright |
| 3 | [upstash/context7](https://github.com/upstash/context7) | ![Stars](https://img.shields.io/github/stars/upstash/context7) | Up-to-date code documentation for LLMs |
| 4 | [makenotion/notion-mcp-server](https://github.com/makenotion/notion-mcp-server) | ![Stars](https://img.shields.io/github/stars/makenotion/notion-mcp-server) | Official Notion integration |
| 5 | [ChromeDevTools/chrome-devtools-mcp](https://github.com/ChromeDevTools/chrome-devtools-mcp) | ![Stars](https://img.shields.io/github/stars/ChromeDevTools/chrome-devtools-mcp) | Chrome DevTools for coding agents |
| 6 | [firecrawl/firecrawl-mcp-server](https://github.com/firecrawl/firecrawl-mcp-server) | ![Stars](https://img.shields.io/github/stars/firecrawl/firecrawl-mcp-server) | Web scraping and search |
| 7 | [cloudflare/mcp-server-cloudflare](https://github.com/cloudflare/mcp-server-cloudflare) | ![Stars](https://img.shields.io/github/stars/cloudflare/mcp-server-cloudflare) | Cloudflare Workers, KV, R2, D1 |
| 8 | [exa-labs/exa-mcp-server](https://github.com/exa-labs/exa-mcp-server) | ![Stars](https://img.shields.io/github/stars/exa-labs/exa-mcp-server) | Exa web search and crawling |
| 9 | [tadata-org/fastapi_mcp](https://github.com/tadata-org/fastapi_mcp) | ![Stars](https://img.shields.io/github/stars/tadata-org/fastapi_mcp) | Expose FastAPI as MCP tools |
| 10 | [modelcontextprotocol/servers/src/sequentialthinking](https://github.com/modelcontextprotocol/servers/blob/main/src/sequentialthinking) | ![Stars](https://img.shields.io/github/stars/modelcontextprotocol/servers) | Official sequential thinking for enhanced reasoning |
| 11 | [GLips/Figma-Context-MCP](https://github.com/GLips/Figma-Context-MCP) | ![Stars](https://img.shields.io/github/stars/GLips/Figma-Context-MCP) | Figma layout info for AI coding |
| 12 | [sooperset/mcp-atlassian](https://github.com/sooperset/mcp-atlassian) | ![Stars](https://img.shields.io/github/stars/sooperset/mcp-atlassian) | Confluence & Jira integration |
| 13 | [idosal/git-mcp](https://github.com/idosal/git-mcp) | ![Stars](https://img.shields.io/github/stars/idosal/git-mcp) | GitMCP - End code hallucinations with real-time GitHub context |
| 14 | [containers/kubernetes-mcp-server](https://github.com/containers/kubernetes-mcp-server) | ![Stars](https://img.shields.io/github/stars/containers/kubernetes-mcp-server) | Kubernetes & OpenShift |
| 15 | [mcp-use/mcp-use](https://github.com/mcp-use/mcp-use) | ![Stars](https://img.shields.io/github/stars/mcp-use/mcp-use) | Fullstack MCP framework |

## Contents

- [Featured - Top 15 Popular MCP Servers](#featured---top-15-popular-mcp-servers)
- [Official](#official)
- [Management Tools](#management-tools)
- [UI & Testing](#ui--testing)
- [Core Servers](#core-servers)
- [Cloud Services](#cloud-services)
- [Database](#database)
- [Browser & Automation](#browser--automation)
- [Search & Scraping](#search--scraping)
- [Development Tools](#development-tools)
- [Communication](#communication)
- [Productivity](#productivity)
- [Clients](#clients)
- [Frameworks & SDKs](#frameworks--sdks)
- [Resources](#resources)

---

## Official

Official MCP specification, SDKs, and reference implementations.

| Project | Stars | Description | Language |
|---------|-------|-------------|----------|
| [modelcontextprotocol/modelcontextprotocol](https://github.com/modelcontextprotocol/modelcontextprotocol) | ![Stars](https://img.shields.io/github/stars/modelcontextprotocol/modelcontextprotocol) | Specification and documentation for MCP | - |
| [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers) | ![Stars](https://img.shields.io/github/stars/modelcontextprotocol/servers) | Official MCP reference servers | TypeScript |
| [modelcontextprotocol/python-sdk](https://github.com/modelcontextprotocol/python-sdk) | ![Stars](https://img.shields.io/github/stars/modelcontextprotocol/python-sdk) | Official Python SDK | Python |
| [modelcontextprotocol/typescript-sdk](https://github.com/modelcontextprotocol/typescript-sdk) | ![Stars](https://img.shields.io/github/stars/modelcontextprotocol/typescript-sdk) | Official TypeScript SDK | TypeScript |
| [modelcontextprotocol/rust-sdk](https://github.com/modelcontextprotocol/rust-sdk) | ![Stars](https://img.shields.io/github/stars/modelcontextprotocol/rust-sdk) | Official Rust SDK | Rust |
| [modelcontextprotocol/swift-sdk](https://github.com/modelcontextprotocol/swift-sdk) | ![Stars](https://img.shields.io/github/stars/modelcontextprotocol/swift-sdk) | Official Swift SDK | Swift |
| [modelcontextprotocol/inspector](https://github.com/modelcontextprotocol/inspector) | ![Stars](https://img.shields.io/github/stars/modelcontextprotocol/inspector) | Visual testing tool for MCP servers | TypeScript |
| [modelcontextprotocol/registry](https://github.com/modelcontextprotocol/registry) | ![Stars](https://img.shields.io/github/stars/modelcontextprotocol/registry) | Community-driven MCP server registry | TypeScript |

---

## Management Tools

Tools for managing, adapting, and integrating MCP servers.

### Server Management & CLI

| Project | Stars | Description |
|---------|-------|-------------|
| [smithery-ai/cli](https://github.com/smithery-ai/cli) | ![Stars](https://img.shields.io/github/stars/smithery-ai/cli) | Install, manage and develop MCP servers and skills |
| [TanStack/cli](https://github.com/TanStack/cli) | ![Stars](https://img.shields.io/github/stars/TanStack/cli) | Official TanStack CLI with MCP server and skills support |

### Adapters & Bridges

| Project | Stars | Description |
|---------|-------|-------------|
| [grll/mcpadapt](https://github.com/grll/mcpadapt) | ![Stars](https://img.shields.io/github/stars/grll/mcpadapt) | Unlock 650+ MCP servers in agentic frameworks |
| [steipete/mcporter](https://github.com/steipete/mcporter) | ![Stars](https://img.shields.io/github/stars/steipete/mcporter) | Call MCPs via TypeScript, masquerading as simple API |
| [langchain-ai/langchain-mcp-adapters](https://github.com/langchain-ai/langchain-mcp-adapters) | ![Stars](https://img.shields.io/github/stars/langchain-ai/langchain-mcp-adapters) | LangChain MCP adapters |
| [SecretiveShell/MCP-actions-adapter](https://github.com/SecretiveShell/MCP-actions-adapter) | ![Stars](https://img.shields.io/github/stars/SecretiveShell/MCP-actions-adapter) | Convert MCP server to GPT Actions compatible API |
| [pawneetdev/rest-to-mcp-adapter](https://github.com/pawneetdev/rest-to-mcp-adapter) | ![Stars](https://img.shields.io/github/stars/pawneetdev/rest-to-mcp-adapter) | Convert REST API specs to MCP tools |

### Protocol Converters

- [pyroprompts/mcp-stdio-to-streamable-http-adapter](https://github.com/pyroprompts/mcp-stdio-to-streamable-http-adapter) - STDIO to Streamable HTTP proxy
- [Moe03/mcp-express-adapter](https://github.com/Moe03/mcp-express-adapter) - Run multiple MCP clients on Express server
- [open-webui/mcpo](https://github.com/open-webui/mcpo) - MCP-to-OpenAPI proxy server

### Skills & Prompt Management

- [microsoft/skills](https://github.com/microsoft/skills) - Microsoft skills, MCP servers, Custom Agents
- [K-Dense-AI/claude-skills-mcp](https://github.com/K-Dense-AI/claude-skills-mcp) - MCP server for searching Claude Agent Skills
- [intellectronica/skillz](https://github.com/intellectronica/skillz) - MCP server for loading skills
- [snyk/agent-scan](https://github.com/snyk/agent-scan) - Security scanner for AI agents and MCP servers

### LangChain Integrations

- [i2y/langchaingo-mcp-adapter](https://github.com/i2y/langchaingo-mcp-adapter) - LangChain Go MCP adapter
- [dshivendra/crewai_mcp_adapter](https://github.com/dshivendra/crewai_mcp_adapter) - CrewAI MCP adapter

---

## UI & Testing

Dashboards, GUIs, and testing tools for MCP servers.

### MCP Dashboards & Managers

| Project | Stars | Description |
|---------|-------|-------------|
| [mcp-router/mcp-router](https://github.com/mcp-router/mcp-router) | ![Stars](https://img.shields.io/github/stars/mcp-router/mcp-router) | Unified MCP Server Management App (1822 stars) |
| [amxv/mcp-manager](https://github.com/amxv/mcp-manager) | ![Stars](https://img.shields.io/github/stars/amxv/mcp-manager) | Simple web UI to manage MCP servers |
| [petiky/mcp-manager](https://github.com/petiky/mcp-manager) | ![Stars](https://img.shields.io/github/stars/petiky/mcp-manager) | Visual client tool for MCP environment management |
| [MediaPublishing/mcp-manager](https://github.com/MediaPublishing/mcp-manager) | ![Stars](https://img.shields.io/github/stars/MediaPublishing/mcp-manager) | Web-based GUI for Claude and Cursor |
| [qdhenry/Claude-Code-MCP-Manager](https://github.com/qdhenry/Claude-Code-MCP-Manager) | ![Stars](https://img.shields.io/github/stars/qdhenry/Claude-Code-MCP-Manager) | Manage MCP configurations for Claude Code |

### MCP Inspectors & Testing Tools

| Project | Stars | Description |
|---------|-------|-------------|
| [modelcontextprotocol/inspector](https://github.com/modelcontextprotocol/inspector) | ![Stars](https://img.shields.io/github/stars/modelcontextprotocol/inspector) | Official visual testing tool for MCP servers |
| [mcp-use/inspector](https://github.com/mcp-use/inspector) | ![Stars](https://img.shields.io/github/stars/mcp-use/inspector) | Modern MCP Inspector for remote MCP servers |
| [lujin3/mcp-inspector](https://github.com/lujin3/mcp-inspector) | ![Stars](https://img.shields.io/github/stars/lujin3/mcp-inspector) | MCP Inspector based on Tauri 2 + Vue 3 |
| [dabit3/mcp-inspector](https://github.com/dabit3/mcp-inspector) | ![Stars](https://img.shields.io/github/stars/dabit3/mcp-inspector) | CLI tool to inspect MCP servers and analyze token costs |

### VSCode Extensions

- [LSTM-Kirigaya/openmcp-client](https://github.com/LSTM-Kirigaya/openmcp-client) - VSCode MCP plugin

---

## Core Servers

Official and reference MCP server implementations.

| Project | Stars | Description |
|---------|-------|-------------|
| [awslabs/mcp](https://github.com/awslabs/mcp) | ![Stars](https://img.shields.io/github/stars/awslabs/mcp) | Official AWS MCP servers |
| [microsoft/mcp](https://github.com/microsoft/mcp) | ![Stars](https://img.shields.io/github/stars/microsoft/mcp) | Microsoft MCP server implementations |
| [github/github-mcp-server](https://github.com/github/github-mcp-server) | ![Stars](https://img.shields.io/github/stars/github/github-mcp-server) | GitHub's official MCP server |
| [googleapis/genai-toolbox](https://github.com/googleapis/genai-toolbox) | ![Stars](https://img.shields.io/github/stars/googleapis/genai-toolbox) | MCP Toolbox for Databases |
| [IBM/mcp](https://github.com/IBM/mcp) | ![Stars](https://img.shields.io/github/stars/IBM/mcp) | IBM MCP servers and developer tools |

---

## Cloud Services

MCP servers for cloud platforms and services.

- [cloudflare/mcp-server-cloudflare](https://github.com/cloudflare/mcp-server-cloudflare) - Cloudflare MCP server
- [makenotion/notion-mcp-server](https://github.com/makenotion/notion-mcp-server) - Official Notion MCP server
- [MicrosoftDocs/mcp](https://github.com/MicrosoftDocs/mcp) - Microsoft Learn MCP server
- [antvis/mcp-server-chart](https://github.com/antvis/mcp-server-chart) - Chart visualization using AntV

---

## Database

MCP servers for database access and management.

- [neo4j-contrib/mcp-neo4j](https://github.com/neo4j-contrib/mcp-neo4j) - Neo4j graph database MCP server
- [qdrant/mcp-server-qdrant](https://github.com/qdrant/mcp-server-qdrant) - Qdrant vector database MCP server
- [containers/kubernetes-mcp-server](https://github.com/containers/kubernetes-mcp-server) - Kubernetes MCP server
- [haris-musa/excel-mcp-server](https://github.com/haris-musa/excel-mcp-server) - Excel file manipulation

---

## Browser & Automation

MCP servers for browser control and automation.

- [microsoft/playwright-mcp](https://github.com/microsoft/playwright-mcp) - Playwright MCP server
- [BrowserMCP/mcp](https://github.com/BrowserMCP/mcp) - Browser control via MCP
- [browserbase/mcp-server-browserbase](https://github.com/browserbase/mcp-server-browserbase) - Browser automation with Browserbase
- [hangwin/mcp-chrome](https://github.com/hangwin/mcp-chrome) - Chrome extension-based MCP server
- [CursorTouch/Windows-MCP](https://github.com/CursorTouch/Windows-MCP) - Windows computer use MCP server

---

## Search & Scraping

MCP servers for web search and content extraction.

- [exa-labs/exa-mcp-server](https://github.com/exa-labs/exa-mcp-server) - Exa web search and crawling
- [firecrawl/firecrawl-mcp-server](https://github.com/firecrawl/firecrawl-mcp-server) - Official Firecrawl web scraping
- [LaurieWired/GhidraMCP](https://github.com/LaurieWired/GhidraMCP) - Ghidra reverse engineering

---

## Development Tools

MCP servers for developer workflows and tooling.

- [sooperset/mcp-atlassian](https://github.com/sooperset/mcp-atlassian) - Atlassian tools (Confluence, Jira)
- [GLips/Figma-Context-MCP](https://github.com/GLips/Figma-Context-MCP) - Figma layout information for AI coding agents
- [svnscha/mcp-windbg](https://github.com/svnscha/mcp-windbg) - WinDBG debugging
- [neka-nat/freecad-mcp](https://github.com/neka-nat/freecad-mcp) - FreeCAD MCP server
- [genomoncology/biomcp](https://github.com/genomoncology/biomcp) - Biomedical data MCP server

---

## Communication

MCP servers for messaging and communication platforms.

- [lharries/whatsapp-mcp](https://github.com/lharries/whatsapp-mcp) - WhatsApp MCP server
- [BeehiveInnovations/pal-mcp-server](https://github.com/BeehiveInnovations/pal-mcp-server) - Multi-model MCP server

---

## Productivity

MCP servers for productivity tools and workflows.

- [tadata-org/fastapi_mcp](https://github.com/tadata-org/fastapi_mcp) - Expose FastAPI as MCP tools
- [open-webui/mcpo](https://github.com/open-webui/mcpo) - MCP-to-OpenAPI proxy server

---

## Clients

Applications and tools that support MCP protocol.

### Desktop Clients

- [indragiek/Context](https://github.com/indragiek/Context) - Native macOS MCP client
- [nbonamy/witsy](https://github.com/nbonamy/witsy) - Desktop AI assistant / universal MCP client
- [daodao97/chatmcp](https://github.com/daodao97/chatmcp) - AI chat client implementing MCP

### CLI Clients

- [adhikasp/mcp-client-cli](https://github.com/adhikasp/mcp-client-cli) - Simple CLI for MCP client
- [jonigl/mcp-client-for-ollama](https://github.com/jonigl/mcp-client-for-ollama) - TUI client for MCP with Ollama
- [zaidmukaddam/scira-mcp-chat](https://github.com/zaidmukaddam/scira-mcp-chat) - Minimalistic MCP client

### Editor/IDE Plugins

- [opensumi/core](https://github.com/opensumi/core) - AI Native IDE with MCP support
- [lizqwerscott/mcp.el](https://github.com/lizqwerscott/mcp.el) - MCP client inside Emacs
- [LSTM-Kirigaya/openmcp-client](https://github.com/LSTM-Kirigaya/openmcp-client) - VSCode MCP plugin

### Game Engine Integration

- [CoplayDev/unity-mcp](https://github.com/CoplayDev/unity-mcp) - Unity Editor MCP integration
- [chongdashu/unreal-mcp](https://github.com/chongdashu/unreal-mcp) - Unreal Engine MCP integration

---

## Frameworks & SDKs

Frameworks and SDKs for building MCP servers and clients.

### TypeScript/JavaScript

| Project | Stars | Description |
|---------|-------|-------------|
| [punkpeye/fastmcp](https://github.com/punkpeye/fastmcp) | ![Stars](https://img.shields.io/github/stars/punkpeye/fastmcp) | TypeScript framework for building MCP servers |
| [basementstudio/xmcp](https://github.com/basementstudio/xmcp) | ![Stars](https://img.shields.io/github/stars/basementstudio/xmcp) | TypeScript MCP framework |
| [QuantGeekDev/mcp-framework](https://github.com/QuantGeekDev/mcp-framework) | ![Stars](https://img.shields.io/github/stars/QuantGeekDev/mcp-framework) | Framework for writing MCP servers in TypeScript |

### Python

| Project | Stars | Description |
|---------|-------|-------------|
| [PrefectHQ/fastmcp](https://github.com/PrefectHQ/fastmcp) | ![Stars](https://img.shields.io/github/stars/PrefectHQ/fastmcp) | Fast, Pythonic way to build MCP servers |
| [mcp-use/mcp-use](https://github.com/mcp-use/mcp-use) | ![Stars](https://img.shields.io/github/stars/mcp-use/mcp-use) | Fullstack MCP framework for AI agents |

### Multi-Language

- [CopilotKit/open-mcp-client](https://github.com/CopilotKit/open-mcp-client) - Open MCP client library

### Agent Frameworks with MCP Support

- [lastmile-ai/mcp-agent](https://github.com/lastmile-ai/mcp-agent) - Build agents using MCP and workflow patterns
- [heurist-network/heurist-agent-framework](https://github.com/heurist-network/heurist-agent-framework) - Flexible AI agent framework with MCP support
- [QwenLM/Qwen-Agent](https://github.com/QwenLM/Qwen-Agent) - Agent framework with MCP, RAG, Chrome extension
- [OpenBMB/UltraRAG](https://github.com/OpenBMB/UltraRAG) - Low-code MCP framework for RAG pipelines
- [SalesforceAIResearch/MCP-Universe](https://github.com/SalesforceAIResearch/MCP-Universe) - Framework for developing and benchmarking AI agents
- [rinadelph/Agent-MCP](https://github.com/rinadelph/Agent-MCP) - Multi-agent system framework via MCP
- [alpic-ai/skybridge](https://github.com/alpic-ai/skybridge) - Framework for building ChatGPT & MCP apps

---

## Resources

Documentation, tutorials, and learning materials.

- [modelcontextprotocol/docs](https://github.com/modelcontextprotocol/docs) - Official MCP documentation
- [leerob/directories](https://github.com/leerob/directories) - Find rules and MCP servers

---

## Contributing

Contributions are welcome! Please read the [contributing guidelines](CONTRIBUTING.md) before submitting PRs.

## License

[![CC0 1.0](https://licensebuttons.net/p/zero/1.0/88x31.png)](http://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, [vivy-yi](https://github.com/vivy-yi) has waived all copyright and related or neighboring rights to this work.
