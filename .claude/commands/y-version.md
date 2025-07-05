# Semantic Version Manager

You apply or update semantic versioning for the current project using a VERSION file and Git tags.

**Command arguments:** `$ARGUMENTS`

## Requirements

You are tasked with applying or updating semantic versioning with the following specifications:

### Core Functionality
- **VERSION file management**: If VERSION file doesn't exist, create it with "0.0.1"
- **Version validation**: Read current version from VERSION file and validate it follows proper semantic versioning (MAJOR.MINOR.PATCH)
- **Git integration**: Create git tags with format "v{version}" and commit with message "Release version {version}"
- **Remote sync**: Push the tag _and_ the version commit to origin after creation

### Supported Commands
Parse the `$ARGUMENTS` and handle these subcommands:

- **`current`** - Display current version without making changes
- **`patch`** - Increment patch version (e.g., 1.2.3 → 1.2.4)
- **`minor`** - Increment minor version and reset patch (e.g., 1.2.3 → 1.3.0)
- **`major`** - Increment major version and reset minor/patch (e.g., 1.2.3 → 2.0.0)
- **`set X.Y.Z`** - Set specific version (e.g., `set 2.1.0`)

### Special Features
- **Dry-run mode**: If `--dry-run` flag is detected in `$ARGUMENTS`, show what would happen **without** making changes
- **Pre-release support**: Handle versions like "1.0.0-alpha.1", "2.0.0-beta.2"
- **Build metadata**: Support build metadata like "1.0.0+build.123"

### Safety Checks
- **Clean working directory**: Verify git working directory is clean before making changes
- **Branch validation**: Optionally check if on main/master branch
- **Error handling**: Handle invalid versions, git issues, network problems gracefully

### Multi-format Updates
If these files exist, also update version in:
- `package.json` (if present)
- `Cargo.toml` (if present)
- `pyproject.toml` (if present)

### Example todo list
- [ ] Check current git status and working directory cleanliness
- [ ] Read current version from VERSION file
- [ ] Increment patch version (X.Y.Z → X.Y.Z)
- [ ] Update VERSION file with new version
- [ ] Check for and update package.json, Cargo.toml, pyproject.toml if present
- [ ] Create git tag with v{version} format
- [ ] Commit changes with proper message
- [ ] Push both commit and tag to origin

### Output Format
For dry-run mode, show:
```
[DRY RUN] Would update version: 1.2.3 → 1.2.4
[DRY RUN] Would update VERSION file
[DRY RUN] Would update package.json
[DRY RUN] Would create git tag: v1.2.4
[DRY RUN] Would commit with message: "Release version 1.2.4"
[DRY RUN] Would push tag to origin

No changes made. Use without --dry-run to apply changes.
```

For successful execution, show:
```
✅ Updated version: 1.2.3 → 1.2.4
✅ Updated VERSION file
✅ Updated package.json
✅ Created git tag: v1.2.4
✅ Committed: "Release version 1.2.4"
✅ Pushed commit and tag to origin
```

### Error Examples
Handle these gracefully:
- Invalid semver format
- Dirty git working directory
- Network issues when pushing
- Missing git repository
- Permission issues

**Always be thorough, robust, and user-friendly with clear success/error messages.**
**Do not create any files other than VERSION if not present**