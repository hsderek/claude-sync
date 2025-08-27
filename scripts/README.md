# Claude State Scripts

This directory contains standalone scripts for managing Claude Code state across multiple projects.

## claude-sync

A completely standalone Python script that syncs Claude-specific documentation and settings from any project to this centralized repository.

### Features

- **Completely Standalone**: Uses system Python with no dependencies
- **Project Independent**: Works with any project without modification
- **No Git Interference**: Uses temporary clones, never touches project git
- **Concurrent Safe**: Multiple projects can sync simultaneously
- **Zero Configuration**: Works with sensible defaults

### Installation

1. Copy `claude-sync` to your project's `scripts/` directory:
```bash
cp /path/to/claude-state/scripts/claude-sync /your/project/scripts/
chmod +x /your/project/scripts/claude-sync
```

2. Add to your project's `.gitignore`:
```
scripts/claude-sync
```

3. Optionally configure in `.env`:
```bash
CLAUDE_STATE_REPO=https://github.com/hsderek/claude-state
CLAUDE_STATE_SUBDIR=your-project-name  # Defaults to directory name
```

### Usage

```bash
# Basic sync (uses defaults from .env or directory name)
/usr/bin/python3 scripts/claude-sync

# With custom message
/usr/bin/python3 scripts/claude-sync --message "feat: Added new functionality"

# Dry run to see what would be synced
/usr/bin/python3 scripts/claude-sync --dry-run

# Override repository
/usr/bin/python3 scripts/claude-sync --repo-url https://github.com/youruser/your-claude-state

# Override subdirectory
/usr/bin/python3 scripts/claude-sync --subdir custom-name
```

### What Gets Synced

The script syncs these files from your project to a subdirectory in this repo:

- `CLAUDE.md` - Main Claude development documentation
- `.claude/` - Claude Code settings and permissions
- `scripts/claude-sync` - The sync script itself (self-documenting)
- `scripts/README.md` - Scripts documentation
- `.vscode/settings.json` - VS Code Claude integration settings
- `docs/DEVELOPER_*.md` - Development documentation files
- `docs/SCRIPT_ARCHITECTURE.md` - Script system documentation
- `docs/CLAUDE_SYNC_WORKFLOW.md` - Sync workflow documentation

### Repository Structure

Each project gets its own subdirectory:

```
claude-state/
├── scripts/              # This directory with standalone scripts
│   ├── claude-sync
│   └── README.md
├── project-1/           # First project's Claude state
│   ├── CLAUDE.md
│   ├── .claude/
│   └── ...
├── project-2/           # Second project's Claude state
│   ├── CLAUDE.md
│   ├── .claude/
│   └── ...
└── another-project/     # Another project's Claude state
    ├── CLAUDE.md
    ├── .claude/
    └── ...
```

### Requirements

- Python 3.6+ (system Python, no venv needed)
- git command available in PATH
- Write access to the claude-state repository

### How It Works

1. **Creates temporary workspace** in `/tmp/`
2. **Clones claude-state repo** to temporary location
3. **Syncs files** to project subdirectory
4. **Commits with message** including project name
5. **Pushes to remote** with retry logic
6. **Cleans up** temporary directory

### Security & Safety

- **Never touches project git**: All git operations in temp directory
- **No credentials stored**: Uses system git credentials
- **Excludes sensitive files**: .env, secrets, logs automatically excluded
- **Temporary operations**: Everything happens in `/tmp/`, cleaned up after

### Troubleshooting

#### Push fails with authentication error
Configure git credentials for the claude-state repository:
```bash
git config --global credential.helper store
# Or use SSH keys with SSH URL
```

#### Script not found
Ensure the script is executable:
```bash
chmod +x scripts/claude-sync
```

#### Python not found
The script uses `/usr/bin/python3`. If Python is elsewhere:
```bash
$(which python3) scripts/claude-sync
```

#### Repository doesn't exist
Create the claude-state repository on GitHub first, then sync.

### Version History

- **v2.0.0** - Complete standalone rewrite
  - No dependencies on project venv or packages
  - Uses only Python standard library
  - Handles both main and master branches
  - Improved concurrent access handling

- **v1.0.0** - Initial version
  - Basic sync functionality
  - Required project dependencies

### Contributing

To update the claude-sync script:

1. Make changes in a project using the script
2. Test thoroughly with dry-run
3. Sync the updated script to this repo
4. Update this README if functionality changes

### License

This script is provided as-is for Claude Code state management. It's designed to be copied and used across projects without restriction.

---

*Last updated from the logreducer project*