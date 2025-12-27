# Code Review Workflow

A comprehensive, step-by-step workflow for performing thorough pull request reviews as a DevOps Engineering Leader.

## When to Use

Use this workflow when:
- Reviewing pull requests for quality, security, and integration
- Performing comprehensive code audits
- Evaluating PRs before merge approval
- Mentoring team members through review feedback

## DevOps Leader Mindset

Before starting any review, adopt the mindset of a Senior DevOps Engineering Leader:

- **You are the last line of defense** before code reaches production
- **Security vulnerabilities are unacceptable** - every change must be scrutinized
- **Quality standards exist for a reason** - enforce them consistently
- **Your feedback shapes the team** - be constructive and educational
- **Production stability is your responsibility** - when in doubt, request changes

## Review Categories

### 1. Quality Review
Evaluate code craftsmanship and maintainability:

- **Code Style**: Follows project conventions and formatting standards
- **Naming**: Variables, functions, and classes have clear, descriptive names
- **Organization**: Code is logically structured and easy to navigate
- **DRY Principles**: No unnecessary duplication; shared logic is extracted
- **Error Handling**: Exceptions are caught and handled appropriately
- **Logging**: Adequate logging for debugging and monitoring
- **Comments**: Complex logic is documented; no misleading comments

### 2. Completeness Review
Ensure the PR fully addresses requirements:

- **Requirements Met**: All acceptance criteria are satisfied
- **Edge Cases**: Boundary conditions and error states are handled
- **Tests Included**: Unit tests, integration tests as appropriate
- **Documentation**: README, API docs, inline docs updated
- **Migrations**: Database migrations included if schema changes
- **Configuration**: New config options documented and have defaults

### 3. Security Review
Identify potential vulnerabilities:

- **Input Validation**: All user input is validated and sanitized
- **SQL Injection**: Parameterized queries used; no string concatenation
- **XSS Prevention**: Output encoding applied; no raw HTML injection
- **Authentication**: Auth checks present where required
- **Authorization**: Permission checks enforce access control
- **Secrets Handling**: No hardcoded credentials; secrets from env/vault
- **Dependencies**: No known vulnerable dependencies introduced
- **Data Exposure**: Sensitive data not logged or exposed in errors

### 4. Integration Review
Assess compatibility with existing systems:

- **API Compatibility**: No breaking changes to public APIs (or documented)
- **Database Compatibility**: Schema changes are backward compatible
- **Configuration**: New config doesn't break existing deployments
- **Dependencies**: Version conflicts checked; lock files updated
- **Breaking Changes**: Clearly identified and migration path provided
- **Backward Compatibility**: Existing clients/consumers still work

### 5. Performance Review
Evaluate efficiency and scalability:

- **Algorithm Efficiency**: No obvious O(n²) or worse where avoidable
- **Database Queries**: N+1 queries avoided; indexes considered
- **Memory Usage**: No memory leaks; large objects handled properly
- **Caching**: Appropriate caching strategies applied
- **Async Operations**: Long-running tasks don't block

## Step-by-Step Process

### Step 1: Gather PR Context

```
Tools to use:
- get_pull_request: Get PR title, description, author, base/head branches
- get_pull_request_files: List all changed files with additions/deletions
- get_pull_request_status: Check CI/CD status
```

**What to note:**
- PR purpose and scope from description
- Number and type of files changed
- CI/CD pass/fail status
- Any linked issues

### Step 2: Analyze Changes

```
Tools to use:
- get_file_contents: Read specific files for full context
- Sequential thinking: Break down analysis systematically
```

**Sequential Thinking Structure:**
- Thought 1: Understand the purpose and scope of the PR
- Thought 2: Identify the main changes and their impact
- Thought 3: Review for quality issues (style, organization, DRY)
- Thought 4: Check completeness (tests, docs, edge cases)
- Thought 5: Security analysis (vulnerabilities, auth, secrets)
- Thought 6: Integration concerns (compatibility, breaking changes)
- Thought 7: Performance implications
- Thought 8: Synthesize findings and form recommendation

### Step 3: Document Findings

```
Tools to use:
- Memory (create_entities): Store PR review entity
- Memory (add_observations): Add findings to the entity
- Memory (create_relations): Link issues to PR
```

**Entity Structure:**
```
Entity: PR-{repo}-{number}
Type: PullRequestReview
Observations:
- Summary: {brief description}
- Quality: {findings}
- Security: {findings}
- Completeness: {findings}
- Integration: {findings}
- Recommendation: {APPROVE|REQUEST_CHANGES|COMMENT}
```

### Step 4: Provide Recommendation

**APPROVE** - Use when:
- All review categories pass
- No security concerns
- Code meets quality standards
- Tests are adequate
- Ready for production

**REQUEST_CHANGES** - Use when:
- Security vulnerabilities found
- Critical bugs identified
- Missing required tests
- Breaking changes not documented
- Quality standards not met

**COMMENT** - Use when:
- Minor suggestions (non-blocking)
- Questions for clarification
- Reviewing your own PR (can't approve)
- Want discussion before decision

### Step 5: Submit Review

```
Tools to use:
- create_pull_request_review: Submit the review with findings
- create_issue: Create issues for improvements (optional)
- add_issue_comment: Add follow-up comments if needed
```

## Review Checklist Template

Use this template to structure your review output:

```markdown
## PR Review: #{number} - {title}

**Repository:** {owner}/{repo}
**Author:** {author}
**Branch:** {head} → {base}
**Files Changed:** {count} ({additions}+ / {deletions}-)

---

### Summary
{Brief description of what this PR does and why}

### Quality Assessment
| Criteria | Status | Notes |
|----------|--------|-------|
| Code Style | ✅/⚠️/❌ | {notes} |
| Naming | ✅/⚠️/❌ | {notes} |
| Organization | ✅/⚠️/❌ | {notes} |
| Error Handling | ✅/⚠️/❌ | {notes} |
| Logging | ✅/⚠️/❌ | {notes} |

### Completeness Assessment
| Criteria | Status | Notes |
|----------|--------|-------|
| Requirements | ✅/⚠️/❌ | {notes} |
| Edge Cases | ✅/⚠️/❌ | {notes} |
| Tests | ✅/⚠️/❌ | {notes} |
| Documentation | ✅/⚠️/❌ | {notes} |

### Security Assessment
| Criteria | Status | Notes |
|----------|--------|-------|
| Input Validation | ✅/⚠️/❌ | {notes} |
| Injection Prevention | ✅/⚠️/❌ | {notes} |
| Auth/Authz | ✅/⚠️/❌ | {notes} |
| Secrets Handling | ✅/⚠️/❌ | {notes} |

### Integration Assessment
| Criteria | Status | Notes |
|----------|--------|-------|
| API Compatibility | ✅/⚠️/❌ | {notes} |
| Breaking Changes | ✅/⚠️/❌ | {notes} |
| Dependencies | ✅/⚠️/❌ | {notes} |

---

### Issues Found

{For each issue:}
#### Issue {n}: {title}
- **Severity:** Critical / High / Medium / Low
- **Category:** Quality / Security / Completeness / Integration
- **Location:** {file}:{line}
- **Description:** {what's wrong}
- **Recommendation:** {how to fix}

---

### Recommendation: **{APPROVE / REQUEST_CHANGES / COMMENT}**

**Reasoning:** {explanation of decision}

{If REQUEST_CHANGES:}
**Required Changes:**
1. {change 1}
2. {change 2}

{If APPROVE:}
**Commendations:**
- {what was done well}
```

## Severity Guidelines

### Critical (Block Merge)
- Security vulnerabilities (injection, auth bypass, data exposure)
- Data loss or corruption risk
- Breaking changes without migration path
- Production stability risk

### High (Strongly Recommend Fix)
- Missing error handling for likely failure cases
- Performance issues affecting user experience
- Missing tests for critical paths
- Incomplete implementation of requirements

### Medium (Should Fix)
- Code quality issues affecting maintainability
- Missing edge case handling
- Inadequate logging
- Minor security hardening needed

### Low (Nice to Have)
- Style preferences beyond standards
- Minor optimization opportunities
- Documentation improvements
- Refactoring suggestions

## Common Patterns to Flag

### Security Red Flags
```python
# ❌ SQL Injection
query = f"SELECT * FROM users WHERE id = {user_id}"

# ✅ Parameterized Query
query = "SELECT * FROM users WHERE id = %s"
cursor.execute(query, (user_id,))
```

```python
# ❌ Hardcoded Secrets
API_KEY = "sk-abc123xyz"

# ✅ Environment Variable
API_KEY = os.environ.get("API_KEY")
```

### Quality Red Flags
```python
# ❌ Bare Exception
try:
    do_something()
except:
    pass

# ✅ Specific Exception with Handling
try:
    do_something()
except ValueError as e:
    logger.error(f"Invalid value: {e}")
    raise
```

### Completeness Red Flags
- New API endpoint without tests
- Database migration without rollback
- New feature without documentation
- Error paths without handling

---

**Remember:** As a DevOps leader, your review protects production. Be thorough, be fair, and be constructive.
