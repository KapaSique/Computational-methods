# Commit Protocol (Auto-loaded)

**APPLIES TO**: All agents, all sessions, all git operations

## Critical Rules

### 1. Author Identity
- **NEVER** add `Co-Authored-By: Claude` or any AI attribution
- Commits are made **ONLY** under user's git identity
- No mentions of AI assistance in commit messages

### 2. Incremental Commits Strategy
Commit progressively as work completes:
- ✅ After each feature implementation
- ✅ After each bug fix
- ✅ After fixing linting/formatting issues
- ✅ After passing tests
- ✅ Between logical work units
- ❌ NOT all at once after everything is done

### 3. Commit Timing
Make commits when:
- User explicitly requests
- Completed a logical unit of work
- Fixed pre-commit hook failures
- About to switch to different task
- Feature/fix is complete and working

### 4. Commit Process

**Step 1 - Check status** (run in parallel):
```bash
git status
git diff
git log --oneline -5
```

**Step 2 - Stage specific files**:
```bash
git add path/to/file1.js path/to/file2.js
```
- Avoid `git add -A` or `git add .`
- Never commit .env, credentials, secrets

**Step 3 - Create commit**:
```bash
git commit -m "$(cat <<'EOF'
type: brief description

Optional details if needed.
EOF
)"
```

**NO Co-Authored-By line!**

**Step 4 - Verify**:
```bash
git status
```

### 5. Pre-commit Hook Failures
If hook fails:
1. Fix the issue
2. Re-stage files
3. Create **NEW** commit (not --amend unless user requests)

### 6. Safety Rules
- ❌ No destructive commands without explicit permission
- ❌ No --no-verify or hook skipping
- ❌ No force push to main/master
- ❌ No git config changes
- ✅ Stage specific files by name

## Application Scope

This protocol is **mandatory** for:
- Main assistant (Kiro)
- All Task-spawned agents (general-purpose, Bash, Explore, Plan)
- All team members
- Any agent performing git operations

**No exceptions.**
