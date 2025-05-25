# Claude Code Custom Commands

This repository contains custom commands for Claude Code that extend its functionality with project-specific automation tools.

## Commands

### Version Command

A semantic version management command that handles versioning for projects using a VERSION file and Git tags.

#### Usage

```bash
> /project:version <subcommand>
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
- **Comprehensive error handling**: Gracefully handles invalid versions, git issues, and network problems
- **Remote sync**: Automatically pushes tags to origin

#### Examples

```bash
# Show current version
> /project:version current

# Increment patch version
> /project:version patch

# Increment minor version
> /project:version minor

# Increment major version
> /project:version major

# Set specific version
> /project:version set 2.1.0

# Preview changes without applying
> /project:version patch --dry-run
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

## Installation

1. Clone this repository to your Claude Code commands directory
2. Ensure the commands are properly configured in your Claude Code setup
3. The version command will be available as `/project:version`

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

All errors are reported with clear, actionable messages to help users resolve issues quickly.