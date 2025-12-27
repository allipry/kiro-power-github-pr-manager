# Code Review Workflow

A comprehensive, step-by-step workflow for performing thorough pull request and merge request reviews as a DevOps Engineering Leader.

## When to Use

Use this workflow when:
- Reviewing pull requests (GitHub, Bitbucket, Azure DevOps)
- Reviewing merge requests (GitLab)
- Performing comprehensive code audits
- Evaluating changes before merge approval
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
Ensure the PR/MR fully addresses requirements:

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
- **Command Injection**: Shell commands properly escaped
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
- **Resource Cleanup**: Connections, files, handles properly closed

## Step-by-Step Process

### Step 1: Gather Context

**Information to collect:**
- PR/MR title and description
- Author and reviewers
- Target branch (main, develop, release)
- List of changed files
- Number of additions/deletions
- CI/CD status (if available)
- Linked issues or tickets

**Questions to answer:**
- What is the purpose of this change?
- What problem does it solve?
- What is the scope of impact?

### Step 2: Analyze Changes

**Use Sequential Thinking to structure your analysis:**

- **Thought 1**: Understand the purpose and scope of the PR/MR
- **Thought 2**: Identify the main changes and their impact
- **Thought 3**: Review for quality issues (style, organization, DRY)
- **Thought 4**: Check completeness (tests, docs, edge cases)
- **Thought 5**: Security analysis (vulnerabilities, auth, secrets)
- **Thought 6**: Integration concerns (compatibility, breaking changes)
- **Thought 7**: Performance implications
- **Thought 8**: Synthesize findings and form recommendation

### Step 3: Document Findings

**Use Memory to store review findings:**

```
Entity: PR-{project}-{number}
Type: CodeReview
Observations:
- Summary: {brief description of changes}
- Quality: {quality findings}
- Security: {security findings}
- Completeness: {completeness findings}
- Integration: {integration findings}
- Performance: {performance findings}
- Recommendation: {APPROVE|REQUEST_CHANGES|COMMENT}
```

**Benefits of storing in memory:**
- Reference when author submits updates
- Track patterns across reviews
- Maintain consistency in feedback
- Build knowledge base of common issues

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

### Step 5: Communicate Feedback

**Structure your feedback clearly:**
1. Start with a summary of what the PR/MR does
2. Acknowledge what was done well
3. List issues by severity (critical first)
4. Provide specific, actionable recommendations
5. End with clear recommendation (approve/changes/comment)

## Review Checklist Template

Use this template to structure your review output:

```markdown
## Code Review: {title}

**Project:** {project/repo}
**Author:** {author}
**Branch:** {source} → {target}
**Files Changed:** {count} ({additions}+ / {deletions}-)

---

### Summary
{Brief description of what this PR/MR does and why}

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

### Performance Assessment
| Criteria | Status | Notes |
|----------|--------|-------|
| Algorithm Efficiency | ✅/⚠️/❌ | {notes} |
| Database Queries | ✅/⚠️/❌ | {notes} |
| Resource Management | ✅/⚠️/❌ | {notes} |

---

### Issues Found

#### Issue 1: {title}
- **Severity:** Critical / High / Medium / Low
- **Category:** Quality / Security / Completeness / Integration / Performance
- **Location:** {file}:{line}
- **Description:** {what's wrong}
- **Recommendation:** {how to fix}

---

### Recommendation: **{APPROVE / REQUEST_CHANGES / COMMENT}**

**Reasoning:** {explanation of decision}

**Required Changes:** (if applicable)
1. {change 1}
2. {change 2}

**Commendations:** (if applicable)
- {what was done well}
```

## Severity Guidelines

### Critical (Block Merge)
- Security vulnerabilities (injection, auth bypass, data exposure)
- Data loss or corruption risk
- Breaking changes without migration path
- Production stability risk
- Compliance violations

### High (Strongly Recommend Fix)
- Missing error handling for likely failure cases
- Performance issues affecting user experience
- Missing tests for critical paths
- Incomplete implementation of requirements
- Potential data integrity issues

### Medium (Should Fix)
- Code quality issues affecting maintainability
- Missing edge case handling
- Inadequate logging
- Minor security hardening needed
- Technical debt introduction

### Low (Nice to Have)
- Style preferences beyond standards
- Minor optimization opportunities
- Documentation improvements
- Refactoring suggestions
- Code clarity enhancements

## Common Patterns to Flag

### Security Red Flags

**SQL Injection:**
```python
# ❌ Vulnerable
query = f"SELECT * FROM users WHERE id = {user_id}"

# ✅ Safe
query = "SELECT * FROM users WHERE id = %s"
cursor.execute(query, (user_id,))
```

**Hardcoded Secrets:**
```python
# ❌ Exposed
API_KEY = "sk-abc123xyz"

# ✅ Secure
API_KEY = os.environ.get("API_KEY")
```

**Command Injection:**
```python
# ❌ Vulnerable
os.system(f"process {user_input}")

# ✅ Safe
subprocess.run(["process", user_input], shell=False)
```

### Quality Red Flags

**Bare Exception:**
```python
# ❌ Swallows errors
try:
    do_something()
except:
    pass

# ✅ Proper handling
try:
    do_something()
except ValueError as e:
    logger.error(f"Invalid value: {e}")
    raise
```

**Magic Numbers:**
```python
# ❌ Unclear
if retry_count > 3:
    raise Exception("Failed")

# ✅ Clear
MAX_RETRIES = 3
if retry_count > MAX_RETRIES:
    raise RetryLimitExceeded(f"Failed after {MAX_RETRIES} attempts")
```

### Completeness Red Flags
- New API endpoint without tests
- Database migration without rollback
- New feature without documentation
- Error paths without handling
- Configuration without defaults

### Performance Red Flags
- N+1 database queries in loops
- Loading entire datasets into memory
- Synchronous operations that should be async
- Missing database indexes for frequent queries
- Unbounded result sets

## Language-Specific Considerations

### Python
- Type hints for function signatures
- Docstrings for public functions
- Use of context managers for resources
- Proper exception hierarchy

### JavaScript/TypeScript
- Proper async/await usage
- Type safety (TypeScript)
- Memory leak prevention (event listeners)
- Proper error boundaries (React)

### Java
- Proper resource management (try-with-resources)
- Null safety considerations
- Thread safety for shared state
- Proper exception handling hierarchy

### Go
- Error handling (don't ignore returned errors)
- Proper goroutine management
- Context propagation
- Defer for cleanup

---

**Remember:** As a DevOps leader, your review protects production. Be thorough, be fair, and be constructive. Your feedback helps the team grow.
