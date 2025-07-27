# Claude Code Custom Commands

This repository contains custom commands for Claude Code that extend its functionality with project-specific automation tools.

**Current Version:** 1.1.0

## Commands

### Version Command

A semantic version management command that handles versioning for projects using a VERSION file and Git tags.

#### Usage

```bash
> /project:y-version <subcommand>
```

#### Subcommands

- **`current`** - Display current version without making changes
- **`patch`** - Increment patch version (e.g., 1.2.3 → 1.2.4)
- **`minor`** - Increment minor version and reset patch (e.g., 1.2.3 → 1.3.0)
- **`major`** - Increment major version and reset minor/patch (e.g., 1.2.3 → 2.0.0)
- **`set X.Y.Z`** - Set specific version (e.g., `set 2.1.0`)

#### Features

- **Automatic VERSION file creation**: Creates VERSION file with "0.0.1" if it doesn't exist
- **Semantic version validation**: Validates proper semver format (MAJOR.MINOR.PATCH)
- **Git integration**: Creates git tags with format "v{version}" and commits with descriptive messages
- **Multi-format support**: Updates version in package.json, Cargo.toml, and pyproject.toml if present
- **Dry-run mode**: Use `--dry-run` flag to preview changes without applying them
- **Pre-release support**: Handles versions like "1.0.0-alpha.1", "2.0.0-beta.2"
- **Build metadata**: Supports build metadata like "1.0.0+build.123"

#### Safety Features

- **Clean working directory check**: Verifies git working directory is clean before making changes
- **Branch validation**: Optional check for main/master branch
- **Error handling**: Gracefully handles invalid versions, git issues, and network problems
- **Remote sync**: Automatically pushes tags to origin

#### Examples

```bash
# In Claude Code

# Show current version
> /project:y-version current

# Increment patch version
> /project:y-version patch

# Increment minor version
> /project:y-version minor

# Increment major version
> /project:y-version major

# Set specific version
> /project:y-version set 2.1.0

# Preview changes without applying
> /project:y-version patch --dry-run
```

#### Output Examples

**Dry-run mode:**
```
[DRY RUN] Would update version: 1.2.3 → 1.2.4
[DRY RUN] Would update VERSION file
[DRY RUN] Would update package.json
[DRY RUN] Would create git tag: v1.2.4
[DRY RUN] Would commit with message: "Release version 1.2.4"
[DRY RUN] Would push tag to origin

No changes made. Use without --dry-run to apply changes.
```

**Successful execution:**
```
✅ Updated version: 1.2.3 → 1.2.4
✅ Updated VERSION file
✅ Updated package.json
✅ Created git tag: v1.2.4
✅ Committed: "Release version 1.2.4"
✅ Pushed tag to origin
```

### Update README Command

A command that automatically updates the README.md file based on recent repository changes and project structure.

#### Usage

```bash
> /project:y-update-readme [custom instructions]
```

#### Features

- **Intelligent analysis**: Analyzes recent git commits, file structure, and existing documentation
- **Content preservation**: Maintains manually written content while updating generated sections
- **Custom instructions**: Accepts additional requirements via arguments
- **Version awareness**: Includes current version from VERSION file
- **Technology detection**: Automatically detects and documents tech stack
- **Link validation**: Ensures internal links work and external links are valid

#### Examples

```bash
# Basic README update
> /project:y-update-readme

# Update with custom instructions
> /project:y-update-readme update copyright information
> /project:y-update-readme add API documentation section
> /project:y-update-readme include deployment instructions
```

#### What Gets Updated

- Project description and current version
- Installation and usage instructions
- API documentation from code analysis
- Dependencies and requirements
- Contributing guidelines and license information
- Technology stack documentation

## Installation

1. Clone this repository to your Claude Code commands directory
2. Commands will be available as:
   - `/project:y-version` - Semantic version management
   - `/project:y-update-readme` - README.md updates
   - `/project:y-attribution` - Add attribution information to README.md
   - `/project:y-giti` - Initialize Git repository with .gitignore

## Requirements

- Git repository with clean working directory
- Appropriate permissions for creating tags and pushing to origin
- Network connectivity for pushing tags to remote repository

## Error Handling

The commands include robust error handling for common scenarios:
- Invalid semantic version formats
- Dirty git working directory
- Network issues when pushing
- Missing git repository
- Permission issues
- File system errors

Vincent Bruijn <vebruijn@gmail.com> • y-a-v-a.org • 2025
