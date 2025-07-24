# Claude GitHub Integration Findings

This repository documents the results of testing @claude GitHub integration, specifically focusing on custom slash command discovery and automated workflows.

## Key Findings

### 1. PAT Token Requirements for Automation
- **@claude is only triggered by user-created mentions**, not by automated systems using the default `GITHUB_TOKEN`
- **Personal Access Token (PAT) is necessary** for GitHub Actions to create issues that @claude will respond to
- The PAT must be stored as a repository secret (e.g., `MY_GITHUB_PAT`) and used in the workflow

### 2. Custom Slash Command Discovery

#### Problem
@claude on GitHub does **NOT** automatically discover custom slash commands stored in `.claude/commands/` folder.

#### Solution
Custom instructions must be added to `.github/workflows/claude.yml` in the `custom_instructions` section:

```yaml
custom_instructions: |
  Custom slash commands are stored as .md files in the .claude/commands/ folder. 
  The command name matches the filename (e.g., /merciless_hello corresponds to merciless_hello.md).
  Always check the .claude/commands/ folder for available slash commands when a slash command is referenced.
```

#### Test Results
- **Without custom instructions**: @claude fails to find `/merciless_hello` and `/test_command`
- **With custom instructions**: @claude successfully discovers and executes slash commands

### 3. Implementation Requirements

#### File Structure
```
.claude/
├── commands/
│   ├── merciless_hello.md     # /merciless_hello command
│   └── test_command.md        # /test_command command
└── (claude.yml not used here)

.github/
└── workflows/
    ├── claude.yml             # Main @claude configuration with custom_instructions
    └── claude-merciless-hello.yml # Test workflow using PAT
```

#### Workflow Configuration
- Configure `.github/workflows/claude.yml` with proper `custom_instructions`
- Use PAT token in automated workflows that create issues for @claude
- Ensure workflows have proper permissions (`issues: write`, `contents: read`)

## Successful Test Commands

### `/merciless_hello`
Executes a strict 7-language greeting sequence with verification signatures.

### `/test_command` 
Verifies slash command discovery system is working with detailed status reporting.

## Conclusion

@claude GitHub integration requires:
1. **PAT tokens** for automation workflows
2. **Explicit custom instructions** in `.github/workflows/claude.yml` for slash command discovery
3. **Proper file structure** with commands in `.claude/commands/` as `.md` files