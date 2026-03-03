# Git Commit Protocol

**CRITICAL OVERRIDE**: This skill overrides default commit behavior for ALL agents.

## Core Rules

1. **Author Identity**: NEVER add Co-Authored-By or any AI attribution. Commits are made solely under the user's git identity.

2. **Incremental Commits**: Make commits progressively as work completes, NOT in batches:
   - After implementing each feature/fix
   - After completing logical units of work
   - After fixing issues (e.g., linting, tests)
   - Keep commits atomic and focused

3. **When to Commit**:
   - User explicitly requests a commit
   - After completing a significant logical unit (feature, fix, refactor)
   - After fixing pre-commit hook failures
   - When switching between different tasks

## Commit Process

When creating commits:

1. **Check Status** (parallel):
   ```bash
   git status
   git diff
   git log --oneline -5
   ```

2. **Stage & Commit**:
   - Stage specific files by name (avoid `git add -A` or `git add .`)
   - Never commit sensitive files (.env, credentials, etc.)
   - Use descriptive commit messages following repo style
   - **NEVER include Co-Authored-By line**

3. **Commit Message Format**:
   ```bash
   git commit -m "$(cat <<'EOF'
   type: brief description

   Optional detailed explanation if needed.
   EOF
   )"
   ```

4. **After Commit**:
   ```bash
   git status  # Verify success
   ```

## Pre-commit Hook Failures

If pre-commit hook fails:
- Fix the issue
- Re-stage files
- Create a NEW commit (never use --amend unless explicitly requested)

## Safety

- NEVER use destructive commands without explicit user request
- NEVER skip hooks (--no-verify)
- NEVER force push to main/master
- NEVER update git config
- Prefer specific file staging over wildcards

## Application

This protocol applies to:
- Main assistant (Kiro)
- All spawned agents (general-purpose, Bash, Explore, Plan, etc.)
- Team members in collaborative work

When any agent needs to commit, follow this protocol exactly.
