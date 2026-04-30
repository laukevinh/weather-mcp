# Weather MCP

## Overview

This is a simple weather MCP following Anthropic's guide: https://modelcontextprotocol.io/docs/develop/build-server

Learn more: https://modelcontextprotocol.io/docs/develop/build-server

## Running as local MCP server

### Windows Client + WSL Server

Here are instructions on how to set up an MCP server in WSL and Claude for Desktop as MCP client in Windows.

Build your MCP server `npm run build`

Install Claude for Desktop for Windows.

Configure Claude for Desktop MCP servers in the `claude_desktop_config.json` file. My file's location was something like `C:\Users\scout\AppData\Local\Packages\Claude_aaa1aaaaaaaaa\LocalCache\Roaming\Claude`. Found it from Claude for Desktop > Settings > Developer > MCP Edit Config.

Add the MCP server under and existing `mcpServers` key or create a new one.

```
{
  "mcpServers": {
    "weather": {
      "command": "node",
      "args": ["\\\\wsl.localhost\\Ubuntu-22.04\\home\\kevin\\weather-mcp\\build\\index.js"]
    }
  }
}
```

Save the file and restart Claude for Desktop.

In chat, check for `weather-mcp` in the `+` icon.

Try asking about the weather where you live.

#### Troubleshooting

Claude for Desktop failed to load MCP. I clicked open the link to logs and saw

```
2026-04-30T22:06:35.691Z [weather-mcp] [info] Server started and connected successfully { metadata: undefined }
'node' is not recognized as an internal or external command,
operable program or batch file.
2026-04-30T22:06:35.739Z [weather-mcp] [error] spawn node ENOENT 
```

I installed node for Windows. Used the Microsoft recommended https://github.com/coreybutler/nvm-windows.

### Claude Code Client + WSL Server

Build your MCP server `npm run build`

Add MCP server to claude code. By default it's local scoped. We'll set to user scope. Read more at https://code.claude.com/docs/en/mcp.

```
claude mcp add --scope user weather-mcp -- node ~/weather-mcp/build/index.js
```

Start up claude and ask about the weather