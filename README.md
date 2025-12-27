# GitHub PR Manager - Kiro Power

A comprehensive Kiro Power for managing GitHub pull requests, performing code reviews, and pushing fixes to repositories with a built-in DevOps leader persona.

## Features

- **Pull Request Management**: Create, review, and manage PRs directly from Kiro
- **Comprehensive Code Reviews**: Structured review process covering quality, security, completeness, and integration
- **DevOps Leader Persona**: Expert code review mindset focused on production stability and security
- **Sequential Thinking**: Methodical analysis for complex code changes
- **Memory Integration**: Track review findings across sessions

## Installation

### From Kiro Powers UI

1. Open Kiro
2. Go to Powers panel
3. Click "Add Custom Power"
4. Select "Git Repository"
5. Enter: `https://github.com/allipry/kiro-power-github-pr-manager`
6. Click "Add"

### Configuration Required

After installation, you **must** configure your GitHub Personal Access Token:

1. Generate a PAT at https://github.com/settings/tokens
2. Select scopes: `repo`, `workflow`
3. Edit the power's `mcp.json` file
4. Replace `YOUR_GITHUB_PAT_HERE` with your actual token

## Usage

### Review a Pull Request

```
Review PR #42 in owner/repo for quality, security, and integration.
Provide a recommendation as a DevOps leader.
```

### Create a Pull Request

```
Create a pull request in owner/repo to fix the bug in app.py.
```

### List Open PRs

```
List open pull requests in owner/repo and summarize their status.
```

## MCP Servers Used

- **@modelcontextprotocol/server-github** - GitHub API operations
- **@modelcontextprotocol/server-sequential-thinking** - Structured analysis
- **@modelcontextprotocol/server-memory** - Review tracking

## Files

- `POWER.md` - Main documentation and configuration guide
- `mcp.json` - MCP server configuration (requires PAT setup)
- `steering/code-review-workflow.md` - Detailed code review process

## License

MIT License - See LICENSE file for details.

## Contributing

Contributions welcome! Please submit PRs for improvements.
