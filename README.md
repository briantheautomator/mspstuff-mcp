# MSPStuff Switchboard: hosted MCP servers for MSPs

Hosted MCP servers for the tools an MSP runs: ConnectWise, NinjaOne, Microsoft 365, SentinelOne, Pax8 and more. Read-only today, every answer traced.

This repository is documentation and directory metadata only. The servers are hosted by MSPStuff; there is nothing here to install or run.

- **Endpoint:** `https://www.mspstuff.io/mcp` (Streamable HTTP)
- **Website:** https://www.mspstuff.io
- **Account:** you need an MSPStuff account. The beta takes applications at https://www.mspstuff.io/beta.

## Connect

Every client points at the same endpoint, `https://www.mspstuff.io/mcp`. Sign in with your MSPStuff account; your admin's scope applies. Setup guides: https://www.mspstuff.io/claude-connectors and https://www.mspstuff.io/ai-connectors.

### Claude.ai

1. Open Settings, then Connectors, then Add custom connector.
2. Name it MSPStuff and paste the endpoint.
3. Approve the request (you sign in with your MSPStuff account), then switch MSPStuff on in a chat.

### Claude Desktop

1. Open Settings, then Connectors, then Add custom connector.
2. Paste the endpoint.
3. Approve the request with your MSPStuff account, then enable it in the chat's tools menu.

### ChatGPT

1. Open Settings, then Connectors, then Create. Developer mode may need turning on for your workspace, and connectors may need your workspace admin.
2. Paste the endpoint as the MCP server URL.
3. Approve the request (you sign in with your MSPStuff account), then start a chat with the connector on.

### Microsoft Copilot Studio

1. In Copilot Studio, open your agent, then Tools, then Add a tool, then Model Context Protocol.
2. Paste the endpoint. Authentication is discovered automatically (OAuth).
3. Approve the request with your MSPStuff account, then publish the agent.

### Claude Code

```sh
claude mcp add --transport http mspstuff https://www.mspstuff.io/mcp
```

Added without a key, Claude Code offers OAuth sign-in on first use. To use a key instead, create one in the MSPStuff app at Settings, Connect your AI (it is shown once), and pass it as a header:

```sh
claude mcp add --transport http mspstuff https://www.mspstuff.io/mcp --header "Authorization: Bearer mspk_YOUR_KEY"
```

Check with `claude mcp list`; `mspstuff` should read as connected.

### Cursor and VS Code

Cursor uses a key. Create one in the MSPStuff app at Settings, Connect your AI (it is shown once), then add this to `~/.cursor/mcp.json`, or `.cursor/mcp.json` in a project, and reload Cursor:

```json
{
  "mcpServers": {
    "mspstuff": {
      "url": "https://www.mspstuff.io/mcp",
      "headers": {
        "Authorization": "Bearer mspk_YOUR_KEY"
      }
    }
  }
}
```

`mspstuff` then appears under Settings, MCP. For VS Code, or any other client that supports remote MCP servers, add a custom remote server with the same URL and the same `Authorization` header. The MSPStuff guides do not cover VS Code menus, so follow your client's own instructions for adding a remote server.

Replace `mspk_YOUR_KEY` with your own key. Never commit a real key.

## Auth

- **OAuth 2.1** with PKCE and dynamic client registration. Claude.ai, Claude Desktop, ChatGPT and Microsoft Copilot use it, and Claude Code can.
- **Protected-resource metadata:** https://www.mspstuff.io/.well-known/oauth-protected-resource. The authorization server is Supabase Auth.
- **Access key:** Cursor, and Claude Code if you prefer, send `Authorization: Bearer mspk_...`.
- `initialize` works without a token. Listing tools needs a signed-in member.

## What it reads

One connection covers every platform your company connected. Each platform has a guide with what it reads and what it does not.

- ConnectWise PSA: https://www.mspstuff.io/integrations/connectwise-psa
- ConnectWise Automate: https://www.mspstuff.io/integrations/connectwise-automate
- ConnectWise RMM (Asio): https://www.mspstuff.io/integrations/connectwise-asio
- ConnectWise ScreenConnect: https://www.mspstuff.io/integrations/connectwise-screenconnect
- NinjaOne: https://www.mspstuff.io/integrations/ninjaone
- Microsoft 365: https://www.mspstuff.io/integrations/microsoft-365
- Google Workspace: https://www.mspstuff.io/integrations/google-workspace
- Cisco Meraki: https://www.mspstuff.io/integrations/meraki
- SentinelOne: https://www.mspstuff.io/integrations/sentinelone
- Webroot: https://www.mspstuff.io/integrations/webroot
- Axcient x360Recover: https://www.mspstuff.io/integrations/axcient
- ImmyBot: https://www.mspstuff.io/integrations/immybot
- Pax8: https://www.mspstuff.io/integrations/pax8
- Xero: https://www.mspstuff.io/integrations/xero
- Ninety: https://www.mspstuff.io/integrations/ninety

In the works, not available yet: Datto RMM, Hudu, Trend Vision One.

All integrations: https://www.mspstuff.io/integrations

Vendor names identify the systems an integration reads. They do not imply a partnership or endorsement.

## Example prompts

- What should I review before Acme's QBR? (PSA agreements, Microsoft 365 licenses, Pax8 invoice lines)
- Which machines in Automate have no SentinelOne agent?
- Compare Acme's Pax8 seats against its assigned Microsoft 365 licenses.
- Which agreements renew this quarter, and what are they worth?
- Which devices haven't checked in for a week, across every organization?
- Which tickets have been open longest on the Help Desk board?

## Read-only and permissions

- Access to your platforms is read-only today. Any change a platform could make is refused by the server before anything reaches the platform.
- What a person can reach depends on the platforms their company connected and what their admin granted, per person and per data area.
- Every answer is traced to the tool call behind it.
- Each person can disconnect a client from the Connect your AI page, which ends its access immediately.

## Links

- Privacy: https://www.mspstuff.io/privacy
- Terms: https://www.mspstuff.io/terms
- Sub-processors: https://www.mspstuff.io/subprocessors
- Security: https://www.mspstuff.io/security
- security.txt: https://www.mspstuff.io/.well-known/security.txt
- Support: https://www.mspstuff.io/support
- Pricing: https://www.mspstuff.io/pricing
- Beta: https://www.mspstuff.io/beta
- Integrations: https://www.mspstuff.io/integrations
- Claude setup guide: https://www.mspstuff.io/claude-connectors

## Directory metadata

- `server.json`: the official MCP Registry entry (`io.mspstuff/switchboard`), with icons.
- `.mcp.json`: a minimal client config for tools that read one from a repository. Cursor also needs the key header shown above.
- `llms-install.md`: short install steps written for AI agents that set up MCP servers.
- `lhm.plugin.json`: the LobeHub MCP marketplace manifest.
- `LICENSE`: MIT.

## License

The MIT license covers the documentation and metadata in this repository, not the hosted MSPStuff service.
