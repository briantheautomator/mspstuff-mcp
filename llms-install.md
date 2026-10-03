# Set up MSPStuff Switchboard

MSPStuff Switchboard is a hosted remote MCP server. There is nothing to install, build or run locally.

1. **Server URL:** `https://www.mspstuff.io/mcp` (Streamable HTTP).
2. **Account:** the person needs an MSPStuff account. The beta takes applications at https://www.mspstuff.io/beta. What the account can reach depends on the platforms its company connected and what its admin granted.
3. **Sign in, one of two ways:**
   - **OAuth** (Claude.ai, Claude Desktop, ChatGPT, Microsoft Copilot Studio, and Claude Code). Add the URL as a remote or custom MCP server and approve the sign-in request with the MSPStuff account. OAuth 2.1 with PKCE and dynamic client registration is discovered automatically.
   - **Access key** (Cursor, or Claude Code if preferred). The person creates a key in the MSPStuff app at Settings, Connect your AI. It is sent as the header `Authorization: Bearer mspk_YOUR_KEY`. The key is shown once.
4. **Claude Code command:** `claude mcp add --transport http mspstuff https://www.mspstuff.io/mcp`
5. **Cursor `~/.cursor/mcp.json`:**

   ```json
   {
     "mcpServers": {
       "mspstuff": {
         "url": "https://www.mspstuff.io/mcp",
         "headers": { "Authorization": "Bearer mspk_YOUR_KEY" }
       }
     }
   }
   ```

6. **Check:** the tool list is available once a member is signed in. Without a signed-in member the server answers `initialize` but lists no tools.

Access is read-only today. Every answer is traced to the tool call behind it. Never ask the user to paste a key into chat; they create it and place it in their own client config.

Full guide: https://github.com/briantheautomator/mspstuff-mcp#connect
