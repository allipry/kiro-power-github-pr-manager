---
name: git-pr-reviewer
displayName: Git PR Reviewer
description: Comprehensive pull request and merge request reviewer for Git platforms. Perform thorough code reviews for quality, security, and integration with a DevOps leader persona.
keywords:
  - git
  - pull-request
  - merge-request
  - code-review
  - devops
  - security
  - quality
author: Kiro Community
---

# Git PR Reviewer Power

A comprehensive power for reviewing pull requests and merge requests across Git platforms with a built-in DevOps leader persona for high-quality, secure code reviews.

## Overview

This power provides structured code review capabilities using sequential thinking and memory:

1. **Sequential Thinking** - Methodical, structured code review analysis
2. **Memory** - Track review findings and recommendations across sessions
3. **DevOps Persona** - Expert code review mindset focused on security and quality

## Platform Support

This power's review methodology works with any Git platform:

- **GitHub** - Pull Requests
- **GitLab** - Merge Requests  
- **Bitbucket** - Pull Requests
- **Azure DevOps** - Pull Requests
- **Gitea/Forgejo** - Pull Requests

The review process and checklists are platform-agnostic. For platform-specific API operations, add the appropriate MCP server to your configuration.

## DevOps Leader Persona

When performing code reviews, this power embodies a **Senior DevOps Engineering Leader** with the following characteristics:

### Role & Responsibilities
- Ultimate authority for PR/MR approvals and merge decisions
- Responsible for code quality, security, and production stability
- Ensures all code meets industry best practices before deployment
- Mentors team members through constructive review feedback

### Review Philosophy
- **Security First**: Every change is evaluated for potential vulnerabilities
- **Quality Over Speed**: Thorough reviews prevent production incidents
- **Constructive Feedback**: Issues are identified with actionable solutions
- **Documentation Matters**: Code should be self-documenting with clear intent

### Standards Enforced
- Clean, maintainable code following project conventions
- Comprehensive error handling and logging
- Security best practices (input validation, auth, secrets management)
- Test coverage for new functionality
- Backward compatibility considerations
- Performance implications assessed

## Capabilities

### Code Review
- Analyze code changes systematically
- Review for:
  - **Quality**: Code style, best practices, maintainability
  - **Completeness**: All requirements addressed, tests included
  - **Security**: Vulnerabilities, injection risks, auth issues
  - **Integration**: Compatibility with existing codebase
  - **Performance**: Efficiency and scalability concerns
- Provide structured recommendations (approve/request changes/reject)

### Review Tracking
- Store review findings in memory for reference
- Track patterns across multiple reviews
- Build knowledge base of common issues
- Reference previous reviews for consistency

### Structured Analysis
- Break down complex changes into manageable steps
- Use sequential thinking for thorough evaluation
- Document reasoning for recommendations
- Provide actionable feedback

## Available Steering Files

- **code-review-workflow** - Detailed step-by-step process for comprehensive PR/MR reviews

## Onboarding

### Prerequisites
- Access to the Git repository being reviewed
- Ability to view code diffs and file changes
- (Optional) Platform-specific MCP server for API operations

### Optional: Platform MCP Servers

For automated API operations, you can add platform-specific MCP servers:

**GitHub:**
```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "YOUR_TOKEN_HERE"
      }
    }
  }
}
```

**GitLab:**
```json
{
  "mcpServers": {
    "gitlab": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-gitlab"],
      "env": {
        "GITLAB_PERSONAL_ACCESS_TOKEN": "YOUR_TOKEN_HERE",
        "GITLAB_API_URL": "https://gitlab.com/api/v4"
      }
    }
  }
}
```

## MCP Config Placeholders

The included `mcp.json` provides sequential-thinking and memory servers. If you add platform-specific servers, replace these placeholders:

- **`YOUR_TOKEN_HERE`**: Your platform's personal access token
  - **GitHub**: Generate at https://github.com/settings/tokens
  - **GitLab**: Generate at https://gitlab.com/-/profile/personal_access_tokens
  - **Bitbucket**: Generate at https://bitbucket.org/account/settings/app-passwords/

## Usage Workflows

### Manual Code Review (Any Platform)

1. **Gather context**: Copy/paste the PR description and file changes
2. **Analyze with Sequential Thinking**: Break down review systematically
3. **Store findings**: Use Memory to track issues found
4. **Provide recommendation**: Structured approve/request changes with reasoning

### Automated Review (With Platform MCP)

1. **Fetch PR details**: Use platform's get_pull_request tool
2. **Get changed files**: Use platform's file diff tools
3. **Analyze with Sequential Thinking**: Methodical review process
4. **Store findings**: Track in Memory
5. **Submit review**: Use platform's review submission tool

### Review from Diff Output

You can paste diff output directly:
```
Review this diff for quality, security, and integration:

diff --git a/src/auth.py b/src/auth.py
index abc123..def456 100644
--- a/src/auth.py
+++ b/src/auth.py
@@ -10,6 +10,10 @@ def authenticate(username, password):
+    # New authentication logic
+    if not validate_input(username):
+        raise ValueError("Invalid username")
...
```

## MCP Servers

This power uses two core MCP servers:

- **sequential-thinking**: Structured analysis for methodical code reviews
- **memory**: Track review findings and recommendations across sessions

Optional platform servers can be added for API operations.

## Example Commands

### Review a PR/MR
```
Review this pull request for quality, security, and integration.
Provide a recommendation as a DevOps leader.

[Paste PR description and diff here]
```

### Review with Context
```
As a DevOps engineering leader, review these changes to the 
authentication module. Focus on security implications.

[Paste code changes]
```

### Track Review Findings
```
Store the findings from this review in memory so I can 
reference them when the author submits updates.
```

### Compare to Previous Reviews
```
Check memory for previous reviews of this component.
Are there recurring issues I should highlight?
```

## Best Practices

### For Reviewers
- Use the code-review-workflow steering file for comprehensive reviews
- Be constructive and specific in feedback
- Approve promptly when standards are met
- Use sequential thinking for complex changes
- Store findings in memory for consistency

### For PR/MR Authors
- Keep changes focused and small (under 400 lines when possible)
- Write clear descriptions explaining the "why"
- Include tests for new functionality
- Self-review before requesting review

### For Teams
- Establish consistent review standards
- Use this power to maintain review quality across reviewers
- Build a knowledge base of common issues in memory
- Reference past reviews for consistency

## Review Categories

### 1. Quality
- Code style and formatting
- Naming conventions
- Code organization and structure
- DRY principles
- Error handling
- Logging and observability

### 2. Completeness
- Requirements addressed
- Edge cases handled
- Tests included
- Documentation updated
- Migrations included (if needed)

### 3. Security
- Input validation
- Injection prevention (SQL, XSS, command)
- Authentication/authorization
- Secrets handling
- Dependency vulnerabilities

### 4. Integration
- API compatibility
- Database compatibility
- Configuration changes
- Breaking changes identified
- Backward compatibility

### 5. Performance
- Algorithm efficiency
- Database query optimization
- Memory management
- Caching strategies
- Async operations

## Troubleshooting

### Memory not persisting
**Cause:** Memory server not running or configured
**Solution:**
1. Verify memory server is in mcp.json
2. Restart Kiro to reload MCP configuration
3. Check MCP server status in Kiro

### Sequential thinking not available
**Cause:** Server not configured or failed to start
**Solution:**
1. Verify sequential-thinking server is in mcp.json
2. Ensure npx can run the package
3. Check for npm/node installation issues

### Platform API errors
**Cause:** Invalid token or permissions
**Solution:**
1. Regenerate your personal access token
2. Ensure token has required scopes (repo access, API access)
3. For self-hosted instances, verify API URL is correct

---

**MCP Servers:** sequential-thinking, memory (+ optional platform servers)
