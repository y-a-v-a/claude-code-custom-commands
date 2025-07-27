---
description: "Initialize a Git repository with a basic .gitignore file"
---

# Git Initialize Command

Initialize a Git repository with a basic .gitignore file.

**Command arguments:** `$ARGUMENTS`

## Requirements

You are tasked with initializing a Git repository with the following specifications:

### Core Functionality
- **Git initialization**: Run `git init` to initialize a new Git repository
- **Gitignore creation**: Create a `.gitignore` file with common file patterns
- **Initial commit**: Commit the `.gitignore` file with message "Add .gitignore"

### Basic .gitignore Content
Include these common patterns:
```
# OS files
.DS_Store
Thumbs.db

# Editor files
.vscode/
.idea/
*.swp
*.swo
*~

# Dependencies
node_modules/
__pycache__/
*.pyc
target/
build/
dist/

# Environment files
.env
.env.local
.env.*.local

# Logs
*.log
logs/

# Temporary files
*.tmp
*.temp
.cache/
```

### Safety Checks
- **Existing repository**: Check if already a Git repository (`.git` directory exists)
- **Existing .gitignore**: Check if `.gitignore` already exists
- **Directory permissions**: Ensure write permissions for creating files

### Output Format
For successful execution:
```
✅ Initialized Git repository
✅ Created .gitignore with basic patterns
✅ Committed .gitignore file
```

For existing repository:
```
ℹ️ Git repository already exists
ℹ️ Skipping git init
```

For existing .gitignore:
```
ℹ️ .gitignore already exists
ℹ️ Skipping .gitignore creation
```

### Error Handling
- **Permission issues**: Handle cases where files cannot be created
- **Git not available**: Check if git command is available
- **Write errors**: Handle filesystem errors gracefully

**Keep the implementation simple and focused on the core task of initializing a Git repository with a basic .gitignore file.**