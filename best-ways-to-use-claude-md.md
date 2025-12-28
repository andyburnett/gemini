# Best Ways to Use CLAUDE.md Files

A comprehensive guide to leveraging CLAUDE.md files for better collaboration with Claude Code.

## What is CLAUDE.md?

CLAUDE.md is a special markdown file that serves as a **memory and knowledge base** for Claude Code. It allows you to document project-specific instructions, coding standards, architectural patterns, and team conventions in one centralized location. Think of it as an onboarding document that Claude automatically reads every time it works on your project.

## Why Use CLAUDE.md?

- **Consistency**: Ensure Claude applies your coding standards and conventions consistently
- **Efficiency**: Avoid repeating common instructions in every conversation
- **Team Alignment**: Share project knowledge with all team members and Claude
- **Automation**: Essential for GitHub Actions where Claude needs to work autonomously
- **Institutional Knowledge**: Capture important patterns and decisions in one place

## Where to Place CLAUDE.md Files

CLAUDE.md files work in a hierarchical system with different scopes and priorities:

| Location | Scope | Priority | Purpose |
|----------|-------|----------|---------|
| `~/.claude/CLAUDE.md` | User-level | Lowest | Your personal preferences across all projects |
| `./CLAUDE.md` | Project root | High | Team-shared project instructions |
| `./.claude/CLAUDE.md` | Project (hidden) | High | Same as above, keeps root cleaner |
| `./.claude/rules/*.md` | Modular rules | High | Topic-specific organized documentation |
| `./CLAUDE.local.md` | Local only | Highest | Personal project preferences (not committed) |

**Most common setup**: Place `CLAUDE.md` in your project root alongside `README.md`.

**For larger projects**: Use `.claude/CLAUDE.md` and organize rules into `.claude/rules/` subdirectories.

## What to Include in CLAUDE.md

### Essential Content

1. **Frequently Used Commands**
   ```markdown
   ## Common Commands
   - Install dependencies: `npm install`
   - Start dev server: `npm run dev`
   - Run tests: `npm test`
   - Build: `npm run build`
   - Deploy: `npm run deploy`
   ```

2. **Code Style Guidelines**
   ```markdown
   ## Code Style
   - Use 2-space indentation (never tabs)
   - Use camelCase for variables and functions
   - Use PascalCase for classes and components
   - Prefix private methods with underscore: `_privateMethod()`
   - Maximum line length: 100 characters
   ```

3. **Architecture and Patterns**
   ```markdown
   ## Architecture
   - Backend follows MVC pattern
   - Frontend uses React with functional components
   - State management: Redux for global state, useState for local
   - API endpoints follow REST conventions
   - Database: PostgreSQL with Prisma ORM
   ```

4. **Testing Standards**
   ```markdown
   ## Testing
   - Write tests for all new features
   - Maintain minimum 80% code coverage
   - Unit tests: Jest
   - Integration tests: Cypress
   - Test files: `__tests__/` directories alongside source
   ```

5. **Git Workflow**
   ```markdown
   ## Git Workflow
   - Main branch is protected, all changes require PRs
   - Branch naming: `feature/*`, `bugfix/*`, `hotfix/*`
   - Commit message format: `[TYPE] Short description`
     - Types: feat, fix, refactor, docs, test, chore
   - Squash commits before merging
   ```

6. **Security Requirements**
   ```markdown
   ## Security
   - Never commit secrets or API keys
   - Use environment variables for configuration
   - All database queries must use parameterized statements
   - Security reviews required for auth/authorization changes
   ```

## Best Practices

### ✅ Do This

- **Be Specific**: Write "Use 2-space indentation" instead of "Format code properly"
- **Use Clear Structure**: Organize with markdown headings and bullet points
- **Document Commands**: Include exact commands for common tasks
- **Explain Why**: Add context about why conventions exist
- **Keep Updated**: Review and update as your project evolves
- **Use Examples**: Show code examples of preferred patterns

### ❌ Avoid This

- **Too Vague**: "Write good code" doesn't give Claude actionable guidance
- **Too Long**: Don't document every detail; focus on essentials
- **Outdated Info**: Remove or update deprecated practices
- **Duplicate Content**: Don't repeat what's already in README.md
- **Personal Rants**: Keep it professional and focused

## Example CLAUDE.md Template

```markdown
# [Project Name] - Development Guidelines

## Project Overview
[Brief description of what this project does and its key components]

## Getting Started
- Install: `npm install`
- Dev server: `npm run dev`
- Tests: `npm test`
- Build: `npm run build`

## Code Style
- Indentation: 2 spaces
- Naming: camelCase for variables, PascalCase for components
- Max line length: 100 characters
- Use async/await instead of promises

## Architecture
- Frontend: React + TypeScript
- State: Redux Toolkit
- Styling: Tailwind CSS
- Backend: Node.js + Express
- Database: PostgreSQL + Prisma

## File Structure
- `/src/components` - React components
- `/src/pages` - Page components
- `/src/hooks` - Custom hooks
- `/src/utils` - Utility functions
- `/src/api` - API client code

## Testing
- All features must include tests
- Use Jest for unit tests
- Use React Testing Library for component tests
- Minimum 80% coverage required

## Git Workflow
- Branch from `main`
- Name branches: `feature/description` or `bugfix/description`
- Commit format: `[type] description`
- Open PR when ready for review
- Squash and merge after approval

## Common Tasks
### Adding a New Feature
1. Create branch: `git checkout -b feature/my-feature`
2. Implement feature with tests
3. Run tests: `npm test`
4. Create PR with description

### Fixing a Bug
1. Create branch: `git checkout -b bugfix/issue-name`
2. Write failing test that reproduces bug
3. Fix bug and verify test passes
4. Create PR referencing issue number
```

## Advanced Features

### Multiple CLAUDE.md Files

Claude loads multiple CLAUDE.md files hierarchically. For example:

```
your-project/
├── CLAUDE.md                      # Main project instructions
├── frontend/
│   └── CLAUDE.md                  # Frontend-specific overrides
└── backend/
    └── CLAUDE.md                  # Backend-specific overrides
```

When working in `frontend/`, Claude loads both the root `CLAUDE.md` AND `frontend/CLAUDE.md`, with the more specific file taking precedence.

### Modular Organization with .claude/rules/

For larger projects, split rules into organized files:

```
your-project/
├── .claude/
│   ├── rules/
│   │   ├── code-style.md          # Style guidelines
│   │   ├── testing.md             # Testing conventions
│   │   ├── security.md            # Security requirements
│   │   ├── frontend/
│   │   │   ├── react.md           # React-specific rules
│   │   │   └── styling.md         # CSS/styling rules
│   │   └── backend/
│   │       ├── api.md             # API design rules
│   │       └── database.md        # Database conventions
```

All `.md` files in `.claude/rules/` are automatically loaded.

### Path-Specific Rules

Use YAML frontmatter to apply rules only to specific files:

```markdown
---
paths: src/api/**/*.ts
---

# API Development Rules

- All endpoints must include input validation
- Use standard error response format
- Include OpenAPI documentation comments
```

### Importing Other Files

Reference other files using `@path` syntax:

```markdown
# Development Guide

See @README for project overview.

See @package.json for available npm commands.

## Additional Documentation
- @docs/architecture.md
- @docs/deployment.md
```

### Local-Only Preferences

Use `CLAUDE.local.md` for personal preferences that shouldn't be committed:

```markdown
# My Personal Preferences (CLAUDE.local.md)

- I prefer verbose error messages during development
- Always run tests before committing
- Use my custom git aliases for commits
```

This file is automatically added to `.gitignore`.

## Quick Start

To get started with CLAUDE.md in your project:

1. **Create the file**:
   ```bash
   touch CLAUDE.md
   ```

2. **Add basic structure**:
   - Project overview
   - Common commands
   - Code style basics
   - Key architectural patterns

3. **Iterate and improve**:
   - Add conventions as you establish them
   - Update when you notice repeated instructions
   - Remove outdated information

4. **Review regularly**:
   - Monthly review during team meetings
   - Update after major architectural changes
   - Keep it relevant and focused

## Additional Resources

- [Claude Code Memory Documentation](https://code.claude.com/docs/en/memory.md)
- [GitHub Actions with CLAUDE.md](https://code.claude.com/docs/en/github-actions.md)
- [CLI Reference](https://code.claude.com/docs/en/cli-reference.md)

---

**Remember**: CLAUDE.md is a living document. Start simple and expand it as your project grows and patterns emerge. The goal is to make collaboration with Claude more efficient and aligned with your team's standards.
