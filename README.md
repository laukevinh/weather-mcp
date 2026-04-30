# Weather MCP

## Overview

This is a simple weather MCP following Anthropic's guide: https://code.claude.com/docs/en/mcp/

## Windows Client + WSL Server

Here are instructions on how to set up an MCP server in WSL and Claude for Desktop as MCP client in Windows.

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

### Troubleshooting

Claude for Desktop failed to load MCP. I clicked open the link to logs and saw

```
2026-04-30T22:06:35.691Z [weather-mcp] [info] Server started and connected successfully { metadata: undefined }
'node' is not recognized as an internal or external command,
operable program or batch file.
2026-04-30T22:06:35.739Z [weather-mcp] [error] spawn node ENOENT 
```

I installed node for Windows. Used the Microsoft recommended https://github.com/coreybutler/nvm-windows.