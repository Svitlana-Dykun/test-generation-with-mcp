# Setup Instructions for Colleagues

## Overview
This repository contains separated system prompts for better organization:
- **MCP-specific rules** (when to use Playwright MCP)
- **General agent behavior rules** (project workflow and testing strategy)
- **Elementor-specific rules** (domain-specific testing patterns)

## Step 1: Copy System Prompts

Copy these files to your local `.cursor/system-prompts/` directory:

```bash
# Create directory if it doesn't exist
mkdir -p ~/.cursor/system-prompts/

# Copy the files
cp .cursor/system-prompts/mcp-rules.md ~/.cursor/system-prompts/
cp .cursor/system-prompts/agent-rules.md ~/.cursor/system-prompts/
cp .cursor/system-prompts/elementor-specific.md ~/.cursor/system-prompts/
cp .cursor/system-prompts/README.md ~/.cursor/system-prompts/
```

## Step 2: Configure MCP Server

### 2.1 Install Playwright MCP Server
```bash
npm install -g @modelcontextprotocol/server-playwright
```

### 2.2 Configure MCP in Cursor

Create or update your MCP configuration file: `~/.cursor/mcp.json`

```json
{
  "mcpServers": {
    "playwright-mcp": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-playwright", "run", "--browser", "chromium"],
      "env": {}
    }
  },
  "mcp.experimental.defaultAgent": "playwright-mcp",
  "mcp.experimental.systemPrompt": ".cursor/system-prompts/mcp-rules.md"
}
```

### 2.3 Alternative: Use Local Installation
If you prefer local installation, update the command in `mcp.json`:

```json
{
  "mcpServers": {
    "playwright-mcp": {
      "command": "node",
      "args": ["./node_modules/@modelcontextprotocol/server-playwright/dist/index.js", "run", "--browser", "chromium"],
      "env": {}
    }
  }
}
```

## Step 3: Restart Cursor

1. **Close Cursor completely**
2. **Reopen Cursor**
3. **Verify MCP is working** by trying a simple MCP command

## Step 4: Test the Setup

### 4.1 Test MCP Connection
Try a simple MCP command to verify everything works:
- Open a test file
- Ask the agent to use MCP to inspect the page
- Verify MCP tools are available

### 4.2 Test Rule Separation
Verify that:
- MCP rules apply when analyzing app behavior
- Agent rules apply for general project workflow
- Elementor rules apply for domain-specific testing

## File Structure Explanation

```
.cursor/system-prompts/
├── mcp-rules.md           # When and how to use Playwright MCP
├── agent-rules.md         # General project workflow and testing strategy
├── elementor-specific.md  # Elementor-specific testing patterns
├── README.md             # Overview and usage guide
└── SETUP-INSTRUCTIONS.md # This file
```

## Usage Guidelines

### When to Use MCP:
- **Phase 1 Analysis**: Exploring widgets/features to create test plans
- **Debugging**: Inspecting actual DOM, iframe, logs, network, styles
- **Understanding Interactions**: Seeing how controls work, element selectors, timing

### When NOT to Use MCP:
- Writing test code based on existing knowledge
- File operations and project management
- Code review and refactoring
- General project workflow tasks

## Troubleshooting

### MCP Not Working?
1. **Check installation**: `npx @modelcontextprotocol/server-playwright --version`
2. **Verify config**: Check `~/.cursor/mcp.json` syntax
3. **Restart Cursor**: Complete restart required after config changes
4. **Check browser**: Ensure Chromium is available

### Rules Not Applying?
1. **Check file paths**: Ensure files are in `~/.cursor/system-prompts/`
2. **Verify config**: Check `mcp.experimental.systemPrompt` path
3. **Restart Cursor**: Rules are loaded on startup

### Permission Issues?
```bash
# Fix permissions if needed
chmod +x ~/.cursor/mcp.json
```

## Additional Notes

- **Backup your existing config** before making changes
- **Test in a simple project first** before using in production
- **Keep the original files** as reference until you're comfortable
- **Ask for help** if something doesn't work as expected
- **Feel free to adjust** the rules and configuration to fit your specific needs and workflow

## Support

If you encounter issues:
1. Check this instruction file first
2. Verify all file paths and configurations
3. Test with a simple MCP command
4. Contact the team for additional support

---

**Happy testing! 🚀**
