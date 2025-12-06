# Claude Code - Practical Tips and Best Practices

How to work effectively with Claude Code - proven techniques and workflows.

## Philosophy of Working with Claude Code

### What Claude Code Does Best

✅ **Excellent:**
- Writing and refactoring code
- Code review and finding bugs
- Writing tests
- Code documentation
- Debugging and error analysis
- Translating between programming languages
- Explaining code
- Automating repetitive tasks

⚠️ **With limitations:**
- Very large refactorings (better in small steps)
- Operations requiring whole project context (token limit)
- Real-time debugging (I don't see runtime state)

❌ **Don't use for:**
- Tasks requiring internet access (without MCP)
- Operations on production databases
- Destructive operations without verification

## Basic Principles of Effective Communication

### 1. Be Specific

❌ **Bad:**
```
Fix this
```

✅ **Good:**
```
In file src/auth.ts the validateToken() function doesn't handle the case
when token is expired. Add expiration time checking and return
appropriate error.
```

### 2. Provide Context

❌ **Bad:**
```
Add validation
```

✅ **Good:**
```
In the registration form (src/components/RegisterForm.tsx) add
email and password validation:
- Email: RFC 5322 format
- Password: min 8 characters, 1 uppercase letter, 1 digit, 1 special character
Use Zod for validation, display errors below the input.
```

### 3. Break Down Large Tasks

❌ **Bad:**
```
Build entire authentication system with JWT, refresh tokens, OAuth,
2FA, password reset, email verification and role-based access control.
```

✅ **Good:**
```
Step 1: Create basic authentication with JWT
Step 2: Add refresh tokens
Step 3: Implement password reset
...
```

Or:
```
First do basic JWT authentication (login/logout/protected routes).
Then we'll talk about the remaining features.
```

### 4. Ask for Explanations

✅ **You can always:**
```
Before you start - explain to me how this code works
```

```
I don't understand why you're using this pattern - explain
```

```
What are alternative approaches to this problem?
```

## Prompting Patterns (Proven Patterns)

### Pattern 1: "Analyze → Plan → Execute"

```
1. Analyze file src/api/users.ts
2. Propose refactoring plan to make it more testable
3. Once I approve the plan, execute the refactoring
```

**Why it works:** You give me a chance to understand context before acting.

### Pattern 2: "Show Example"

```
Write tests for calculateDiscount function in src/utils/pricing.ts.

Example test I like:
[example code]

Do similar for remaining cases.
```

**Why it works:** I see your preferred style and conventions.

### Pattern 3: "Iterative Improvement"

```
[Round 1]
Write basic function to parse CSV

[Round 2]
Add error handling and validation

[Round 3]
Add support for custom delimiters

[Round 4]
Optimize for large files (streaming)
```

**Why it works:** Small, controlled steps. Easier to test and verify.

### Pattern 4: "Get Inspired"

```
See how logging is implemented in src/services/logger.ts.

Create similar service for caching, keeping the same pattern
and code style.
```

**Why it works:** You maintain consistency in the project.

### Pattern 5: "Debug with Me"

```
I have an error: [paste error]

Code causing error: [file path]

What I tried: [list of things]

Help me understand what's happening and how to fix it.
```

**Why it works:** Full context = faster diagnosis.

### Pattern 6: "Domain Expert"

```
You're an expert in React performance. Review component
src/components/DataTable.tsx and find all places where
we can improve performance. Explain each optimization.
```

**Why it works:** I focus on a specific aspect.

## Workflow Patterns (Proven Work Flows)

### Workflow 1: Feature Development

```bash
# 1. Planning
"I want to add feature X. What files will I need to change/create?
 Propose architecture."

# 2. Implementation (small steps)
"Let's start with data model"
"Now add API endpoint"
"Now frontend component"

# 3. Tests
"Write tests for what we created"

# 4. Documentation
"Add documentation and update README"

# 5. Review
"Review the entire feature - can anything be improved?"
```

### Workflow 2: Bug Fixing

```bash
# 1. Reproduction
"I have a bug: [description]. Help find where the problem is."

# 2. Analysis
"Analyze [file] and explain why this is happening"

# 3. Fix
"Fix the bug, keeping existing functionality"

# 4. Test
"Write test that verifies the bug is fixed"

# 5. Verify
"Check if fix doesn't introduce regression in other places"
```

### Workflow 3: Refactoring

```bash
# 1. Analysis
"Analyze [file/module] and find code smells"

# 2. Plan
"Propose refactoring plan (what and why)"

# 3. Tests (first!)
"Before refactoring - write tests for current functionality"

# 4. Refactor (small steps)
"Refactor function X"
"Now function Y"

# 5. Verify
"Run tests - everything should pass"
```

### Workflow 4: Code Review

```bash
# As reviewer
"Review PR in files: [list]. Look for:
 - Bugs
 - Security issues
 - Performance problems
 - Code style violations
 - Missing tests
 Format as GitHub review comments."

# As author before PR
"Do self-review of my changes and tell me what I should improve
 before submitting PR"
```

### Workflow 5: Learning Codebase

```bash
# Exploring new project
"Analyze project structure and explain:
 - What is the architecture
 - What are the main modules
 - How does data flow work
 - Where are the entry points"

"Explain to me how feature X works step by step"

"Find all places where function Y is used"
```

## Working with Code

### Good Practices

#### 1. Always Provide Paths

✅ **Good:**
```
Refactor getUserData function in src/api/users.ts
```

❌ **Bad:**
```
Refactor getUserData function
```

#### 2. Specify What Should Be Preserved

✅ **Good:**
```
Refactor, but keep:
- Current interface
- Error handling
- Backwards compatibility
```

#### 3. Define Quality Standard

✅ **Good:**
```
Code should:
- Have type safety (TypeScript strict mode)
- Be covered by tests (min 80%)
- Have JSDoc for public functions
- Follow our style guide in docs/STYLE.md
```

#### 4. Ask for Explanations

✅ **Always OK:**
```
Add comments explaining why this code is written this way
```

```
After implementation - explain to me key decisions you made
```

### Working with Errors

#### When You Get an Error

```
I ran the code and got error:
[full stack trace]

Command I ran:
[command]

Context:
[what I was trying to do]
```

**Not:**
```
Doesn't work
```

#### When Something Works Incorrectly

```
Function returns incorrect result.

Expected: [what should be]
Actual: [what is]
Input: [what input data]

Code: src/utils/calculate.ts:42
```

### Working with Large Changes

#### When Project Is Large

```
# Instead of "review entire project"
Review authentication module (src/auth/**) and find potential
security issues.
```

```
# Instead of "refactor everything"
Refactor src/api/users.ts first, then we'll talk about next ones.
```

#### "Divide and Conquer" Strategy

```
# Step 1: Overview
Analyze src/services/ and tell which files need refactoring.

# Step 2: Prioritization
Which are most important? Propose order.

# Step 3: Execution
OK, starting with [file1]
```

## Working with Tests

### Pattern: Test-Driven Development

```bash
# 1. Write test (red)
"Write test for calculateShipping function that:
 - For weight < 1kg returns 5.00
 - For 1-5kg returns 10.00
 - For >5kg returns 15.00 + 2.00 for each additional kg"

# 2. Implement (green)
"Now implement function so tests pass"

# 3. Refactor
"Optimize implementation keeping tests passing"
```

### Pattern: Existing Code

```bash
"Write tests for existing validateEmail function in src/utils/validation.ts.
 Cover all edge cases."
```

### Pattern: Test Coverage

```bash
"Review file src/api/orders.ts and write tests for all
 functions that don't have tests. Coverage should be >80%."
```

## Git Workflow with Claude

### Commit Messages

```bash
# Good prompt
"I made changes in [files]. Generate commit message according to
 Conventional Commits (feat/fix/docs/etc)."

# Claude generates:
feat(auth): add email verification

- Implement email verification service
- Add verification email template
- Add verification endpoint
- Update user model with verified flag

Closes #123
```

### Code Review before Commit

```bash
"Before commit - review my changes in src/ and tell if
 you see any issues."
```

### Pre-commit Hook Ideas

```bash
"Propose pre-commit hook that:
 - Runs tests
 - Checks linting
 - Verifies commit message is Conventional Commits
 - Blocks commit if something doesn't pass"
```

## Documentation

### Pattern: Auto-Documentation

```bash
"Add JSDoc/docstrings for all public functions in src/api/users.ts.
 Format:
 - Function description
 - @param with types and description
 - @returns with description
 - @throws if applicable
 - @example with concrete usage example"
```

### Pattern: README Generation

```bash
"Generate README.md for this project containing:
 - Project description
 - Installation
 - Usage with examples
 - API documentation
 - Development guide
 - Contributing guidelines"
```

### Pattern: Architecture Documentation

```bash
"Generate docs/ARCHITECTURE.md describing:
 - Project structure
 - Main modules and their responsibilities
 - Data flow
 - Most important architectural decisions and why"
```

## Debugging

### Effective Debugging with Claude

#### 1. Full Context

```
Problem: [specific description]
Error: [full error message + stack trace]
Code: [file path or snippet]
What I tried: [list of attempts]
Environment: [Node 18, Ubuntu 22.04, etc]
```

#### 2. Systematic Approach

```
"Help me debug this problem systematically:

1. First analyze code and explain what should happen
2. Then check where problem might be
3. Propose way to diagnose (console.log, debugger, etc)
4. When we find problem, propose fix"
```

#### 3. Interactive Debugging

```
[After each debugging step I provide results]

You: "Add console.log before line 42 and tell me what displays"
Me: [result]
You: "OK, now check value of X"
Me: [result]
...iteratively
```

## Performance Optimization

### Pattern: Profile → Analyze → Optimize

```bash
# 1. Identify
"Analyze src/components/DataGrid.tsx for performance.
 Find potential bottlenecks."

# 2. Measure
"Add performance measurements to verify problem"

# 3. Optimize
"Optimize [specific function/component]"

# 4. Verify
"Check if optimization doesn't break functionality (add tests)"
```

### Pattern: Bundle Size

```bash
"Analyze bundle size:
 1. What are the largest dependencies?
 2. What can we tree-shake?
 3. What can be lazy-loaded?
 4. Propose specific optimizations"
```

## Security

### Security Review

```bash
"Review code for security:
 - SQL injection
 - XSS
 - CSRF
 - Authentication/Authorization issues
 - Sensitive data exposure
 - Dependency vulnerabilities

For each finding:
 - Severity (Critical/High/Medium/Low)
 - Location
 - Problem description
 - How to fix"
```

### Secret Scanning

```bash
"Check if project has:
 - API keys
 - Passwords
 - Tokens
 - Private keys
 - Credentials

If you find any - tell me where and suggest how it should be."
```

## Anti-Patterns (What to Avoid)

### ❌ Too General Requests

```
"Improve code"
"Optimize this"
"Fix bugs"
```

**Better:**
```
"Optimize for memory usage"
"Fix TypeScript errors"
"Improve error handling"
```

### ❌ Without Context

```
"Why doesn't this work?"
```

**Better:**
```
"Function X in file Y returns undefined instead of expected value Z.
 Input is A, B, C. Help find problem."
```

### ❌ Everything at Once

```
"Build entire e-commerce application with backend, frontend, database,
 authentication, payments, and deploy to AWS"
```

**Better:**
```
"Let's start with basic API for products. First data model
 and basic CRUD endpoints."
```

### ❌ Lack of Verification

```
[Claude did something]
[Commits without checking]
[Turns out it doesn't work]
```

**Better:**
```
[Claude did something]
[I test]
"Works, but I have question about line 42 - why..."
[Discussion/fixes]
[Commit]
```

## Advanced Techniques

### Chain of Thought Prompting

```
"Solve this problem step by step:

1. First explain problem in your own words
2. List all possible solutions
3. Evaluate pros/cons of each
4. Choose best and explain why
5. Implement"
```

### Few-Shot Learning

```
"Write function to validate phone number.

Example of similar code in our project:
[email validation example]

Do analogously, keeping same style and pattern."
```

### Constrained Output

```
"Generate code that:
✓ MUST use TypeScript strict mode
✓ MUST have error handling
✓ MUST be <100 lines
✓ CANNOT use any
✓ CANNOT have side effects
"
```

### Meta-Prompting

```
"Before you answer, think:
- Do I understand the problem well?
- Do I have all necessary information?
- What assumptions am I making?

If something is missing - ask me first."
```

## Productivity Boosters

### 1. Use Slash Commands

```bash
# Instead of describing every time
/review src/api/users.ts

# Custom command does:
# - Code review
# - Find bugs
# - Check best practices
# - Suggest improvements
```

### 2. Template Prompts

Create `.claude/prompts/` with ready-made:

**refactor.md:**
```
Refactor {{file}} to be:
- More readable
- Better testable
- DRY (no duplication)
- SOLID compliant

Explain each significant change.
```

**security-check.md:**
```
Security review for {{file}}:
- Input validation
- SQL injection
- XSS
- Authentication/Authorization
- Sensitive data handling
```

### 3. Iterative Workflow

```bash
# Instead of everything at once:
"Write api + tests + docs for feature X"

# Do iteratively:
[Round 1] "Write API endpoint"
[Test] curl ...
[Round 2] "Add tests"
[Test] npm test
[Round 3] "Add documentation"
```

### 4. Leverage Context

```bash
# During longer session:
"Remember function X we wrote earlier?
 Now do similarly for Y"

"Using same pattern as in previous file..."
```

## Quick Tips

### Communication

- 🎯 Be specific
- 📍 Provide locations (file paths)
- 📝 Describe expected behavior
- ❓ Ask for explanations
- 🔄 Iterate (small steps)

### Code

- ✅ Always test
- 📚 Ask for documentation
- 🔍 Do code review
- 🧪 TDD when possible
- 📦 Small, atomic changes

### Workflow

- 📋 Plan before acting
- 🔄 Iterate, don't do everything at once
- ✓ Verify each step
- 💾 Commit often
- 📖 Document decisions

## Example Session (Best Practices)

```
You: "I want to add feature: user notifications in React+Node.js app"

Claude: "OK, let's plan:
1. Backend: API endpoints + database model
2. Frontend: UI components
3. Real-time: WebSocket integration
4. Tests
5. Documentation

Where do we start?"

You: "Let's start with backend. What endpoints will we need?"

Claude: [analysis + proposal]

You: "OK, let's do database model first"

Claude: [model implementation]

You: "Great. Now API endpoints for CRUD notifications"

Claude: [implementation]

You: "Add tests for these endpoints"

Claude: [tests]

You: "Review what we did and tell if anything can be improved"

Claude: [code review + suggestions]

You: "OK, implement suggestion #2"

Claude: [refactor]

You: "Generate commit message"

Claude: [conventional commits message]

You: "Now we can move to frontend"
...
```

## Resources

- **Documentation:** https://code.claude.com/docs
- **GitHub Discussions:** https://github.com/anthropics/claude-code/discussions
- **Prompt Engineering Guide:** https://www.promptingguide.ai/

## Quick Cheat Sheet

```bash
✅ DO:
- Be specific and detailed
- Provide full context
- Break large tasks into small ones
- Test and verify
- Ask for explanations
- Iterate and improve

❌ DON'T:
- General requests without context
- Everything at once
- Commit without testing
- Assume Claude knows everything about project
- Skip edge cases
```

**Remember:**
- I'm a tool - You are the developer
- Always verify what I do
- Small steps = fewer errors
- Communication > magical thinking
- Iteration > perfection on first try
