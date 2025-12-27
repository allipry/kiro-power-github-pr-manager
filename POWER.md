---
name: github-pr-manager
displayName: GitHub PR Manager
description: Create, review, and manage pull requests in GitHub repositories. Perform comprehensive code reviews for quality, security, and integration with a DevOps leader persona.
keywords:
  - github
  - pull-request
  - pr
  - code-review
  - repository
  - branch
  - merge
  - devops
  - commit
author: Kiro Community
---

# GitHub PR Manager Power

A comprehensive power for managing GitHub pull requests, performing code reviews, and pushing fixes to repositories - with a built-in DevOps leader persona for high-quality, secure code reviews.

## Overview

This power combines the GitHub MCP server with sequential thinking and memory to provide:

1. **GitHub Operations** - Create branches, commits, and pull requests
2. **Sequential Thinking** - Structured code review and analysis
3. **Memory** - Track review findings and recommendations across sessions
4. **DevOps Persona** - Expert code review with security and quality focus

## DevOps Leader Persona

When performing code reviews, this power embodies a **Senior DevOps Engineering Leader** with the following characteristics:

### Role & Responsibilities
- Ultimate authority for PR approvals and merge decisions
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

### Pull Request Creation
- Create branches in repositories you control
- Push file changes directly to GitHub
- Create pull requests with detailed descriptions
- Update existing PRs with additional commits

### Code Review
- Fetch and analyze PR diffs
- Review code for:
  - **Quality**: Code style, best practices, maintainability
  - **Completeness**: All requirements addressed, tests included
  - **Security**: Vulnerabilities, injection risks, auth issues
  - **Integration**: Compatibility with existing codebase
- Provide structured recommendations (approve/request changes/reject)

### Repository Management
- List and search repositories
- View file contents and history
- Compare branches
- Manage issues linked to PRs

## Available Steering Files

- **code-review-workflow** - Detailed step-by-step process for comprehensive PR reviews

## Onboarding

### Prerequisites
- GitHub account with access to target repositories
- GitHub Personal Access Token (PAT) with appropriate scopes

### GitHub Personal Access Token (PAT) Setup

You need a GitHub PAT with the following scopes:
- `repo` - Full control of private repositories
- `workflow` - Update GitHub Action workflows (if needed)

**To create a PAT:**
1. Go to GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Click "Generate new token (classic)"
3. Give it a descriptive name (e.g., "Kiro PR Manager")
4. Select scopes: `repo`, `workflow`
5. Click "Generate token"
6. Copy the token (starts with `ghp_`)

**Important:** Store your token securely. You'll need it for the mcp.json configuration.

## MCP Config Placeholders

**IMPORTANT:** Before using this power, replace the following placeholder in `mcp.json` with your actual value:

- **`YOUR_GITHUB_PAT_HERE`**: Your GitHub Personal Access Token
  - **How to get it:**
    1. Go to https://github.com/settings/tokens
    2. Click "Generate new token (classic)"
    3. Select scopes: `repo`, `workflow`
    4. Copy the generated token (starts with `ghp_`)
    5. Paste it in place of `YOUR_GITHUB_PAT_HERE`

**After replacing the placeholder, your mcp.json should look like:**
```json
{
  "mcpServers": {
    "github": {
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_your_actual_token_here"
      }
    }
  }
}
```

## Usage Workflows

### Creating a PR for a Fix

1. **Identify the fix needed** in the target repository
2. **Create a branch**: Use `create_branch` tool
3. **Push changes**: Use `push_files` or `create_or_update_file` tool
4. **Create PR**: Use `create_pull_request` tool with detailed description

### Reviewing a PR

1. **Fetch PR details**: Use `get_pull_request` tool
2. **Get changed files**: Use `get_pull_request_files` tool
3. **Analyze with Sequential Thinking**: Break down review into structured steps
4. **Store findings**: Use Memory to track issues found
5. **Provide recommendation**: Submit review with approve/request changes

### Managing Issues

1. **List issues**: Use `list_issues` tool to see open issues
2. **Create issue**: Use `create_issue` for bugs or improvements found during review
3. **Link to PR**: Reference issues in PR descriptions

## MCP Servers

This power uses three MCP servers:

- **github**: GitHub API operations (branches, commits, PRs, files, issues)
- **sequential-thinking**: Structured analysis for methodical code reviews
- **memory**: Track review findings and recommendations across sessions

## Example Commands

### Review a PR
```
Review PR #42 in owner/repo for quality, security, and integration. 
Provide a recommendation as a DevOps leader.
```

### Create a fix PR
```
Create a pull request in owner/repo to fix the bug in app.py 
where the configuration is missing validation.
```

### Check PR status
```
List open pull requests in owner/repo and summarize their status.
```

### Create an issue for improvements
```
Create an issue in owner/repo for the refactoring suggestions 
identified during the PR review.
```

## Best Practices

### For PR Authors
- Keep PRs focused and small (under 400 lines when possible)
- Write clear PR descriptions explaining the "why"
- Include tests for new functionality
- Self-review before requesting review

### For Reviewers
- Use the code-review-workflow steering file for comprehensive reviews
- Be constructive and specific in feedback
- Approve promptly when standards are met
- Use sequential thinking for complex changes

### For Repository Maintainers
- Set up branch protection rules
- Require PR reviews before merging
- Use this power to maintain consistent review quality

## Troubleshooting

### Error: "Bad credentials"
**Cause:** Invalid or expired GitHub PAT
**Solution:**
1. Generate a new PAT at https://github.com/settings/tokens
2. Update the token in mcp.json
3. Restart Kiro to reload MCP configuration

### Error: "Not Found" when accessing repository
**Cause:** PAT doesn't have access to the repository
**Solution:**
1. Ensure PAT has `repo` scope
2. For organization repos, ensure SSO is authorized if required
3. Verify you have access to the repository in GitHub

### Error: "Review Can not approve your own pull request"
**Cause:** GitHub doesn't allow self-approval of PRs
**Solution:** Submit review as COMMENT instead of APPROVE for your own PRs

---

**MCP Servers:** github, sequential-thinking, memory
