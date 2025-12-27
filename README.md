# Git PR Reviewer - Kiro Power

A comprehensive Kiro Power for reviewing pull requests and merge requests across Git platforms with a built-in DevOps leader persona.

## Features

- **Platform Agnostic**: Works with GitHub, GitLab, Bitbucket, Azure DevOps, and more
- **Comprehensive Code Reviews**: Structured review process covering quality, security, completeness, integration, and performance
- **DevOps Leader Persona**: Expert code review mindset focused on production stability and security
- **Sequential Thinking**: Methodical analysis for complex code changes
- **Memory Integration**: Track review findings across sessions for consistency

## Installation

### From Kiro Powers UI

1. Open Kiro
2. Go to Powers panel
3. Click "Add Custom Power"
4. Select "Git Repository"
5. Enter: `https://github.com/allipry/kiro-power-github-pr-manager`
6. Click "Add"

### No Configuration Required

This power works out of the box with sequential-thinking and memory servers. No API tokens needed for basic usage.

### Optional: Platform API Integration

For automated API operations, add platform-specific MCP servers to your configuration. See POWER.md for examples.

## Usage

### Review Code Changes

```
Review this pull request for quality, security, and integration.
Provide a recommendation as a DevOps leader.

[Paste PR description and diff here]
```

### Review with Focus Area

```
As a DevOps engineering leader, review these changes to the 
authentication module. Focus on security implications.

[Paste code changes]
```

### Track Findings

```
Store the findings from this review in memory so I can 
reference them when the author submits updates.
```

## MCP Servers Used

- **@modelcontextprotocol/server-sequential-thinking** - Structured analysis
- **@modelcontextprotocol/server-memory** - Review tracking

## Files

- `POWER.md` - Main documentation and usage guide
- `mcp.json` - MCP server configuration
- `steering/code-review-workflow.md` - Detailed code review process

## Review Categories

1. **Quality** - Code style, naming, organization, error handling
2. **Completeness** - Requirements, tests, documentation, edge cases
3. **Security** - Input validation, injection prevention, auth, secrets
4. **Integration** - API compatibility, breaking changes, dependencies
5. **Performance** - Algorithm efficiency, queries, resource management

## License

MIT License - See LICENSE file for details.

## Contributing

Contributions welcome! Please submit PRs for improvements.
