# Streamlining Development Workflows with Claude Code Custom Commands

I recently discovered a neat feature in Anthropic's [Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview): custom slash commands. I wanted a way to easily tag repository states, and specifically in small projects that do not rely on `package.json` or similar, by relying on a `VERSION` file. I decided to dive into custom slash commands and create my own semantic versioning command. What I found was a flexible system that has lightened up how I handle routine development tasks.

## The Problem: Repetitive Version Management

I love Git, it's ondoubtedly very powerful, but the tedious process of versioning was something I stopped doing because of all steps I wanted to take, for example:

1. Check if the working directory is clean
2. Read the current version from a `VERSION` file
3. Increment the version according to semantic versioning rules
4. Update the `VERSION` file
5. Create a git tag
6. Commit the changes
7. Push everything to the remote repository

This process, while straightforward, was error-prone and time-consuming. I want to rely more on `VERSION` file updates to trigger [GitHub Actions](https://github.com/features/actions) workflows for automated deployments and releases: I wanted something more automated, more reliable, and frankly, more elegant.

## Enter Claude Code Custom Commands

Claude Code's custom slash commands feature allows you to create reusable prompts that can be shared across your team or kept personal. There are two types:

- **Project commands** (`.claude/commands/`): Shared with your team using `/project:command-name`
- **Personal commands** (`~/.claude/commands/`): Available across all your projects using `/user:command-name`

The beauty lies in their simplicity. You create a Markdown file with your command specification, and Claude Code handles the rest.

## Building a Semantic Version Manager

I decided to create a comprehensive version management command. Here's what I built:

```markdown
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
```

The magic happens with the `$ARGUMENTS` placeholder. This allows the command to be flexible and handle different subcommands dynamically.

## Real-World Usage

Now, instead of going through that lengthy manual process, I simply type:

```bash
/project:y-version patch
```

And Claude Code handles everything:

```
✅ Updated version: 1.0.0 → 1.0.1
✅ Updated VERSION file
✅ Updated package.json
✅ Created git tag: v1.0.1
✅ Committed: "Release version 1.0.1"
✅ Pushed commit and tag to origin
```

For major releases, it's just as simple:

```bash
/project:y-version major
```

The command even includes safety features like checking for a clean working directory and graceful error handling.

## Advanced Features I Added

What started as a simple version incrementer evolved into a robust tool:

- **Dry-run mode**: Preview changes without applying them using `--dry-run`
- **Multi-format support**: Automatically updates `package.json`, `Cargo.toml`, and `pyproject.toml` if present
- **Pre-release support**: Handles versions like "1.0.0-alpha.1"
- **Build metadata**: Supports build metadata like "1.0.0+build.123"
- **Comprehensive error handling**: Gracefully handles network issues, permission problems, and invalid version formats

## Lessons Learned: Precision in Prompt Engineering

Creating this command required several iterations to get right. Initially, Claude Code would eagerly interpret "implementing semantic version management" as a request to write a fresh bash script for version management - clearly not what I wanted! The solution was changing the wording to "applying semantic version management" which guided Claude to work with existing tools rather than creating new ones.

I also had to add an explicit instruction: "Do not create any files other than `VERSION` if not present" to prevent the creation of unnecessary bash scripts. These refinements highlight how precise language in custom commands can make the difference between a helpful automation tool and an overzealous code generator.

It proves again that one needs to be very specific in prompts in natural language.

## The Bigger Picture

Custom slash commands have proven to be incredibly flexible! I've created a Github repository for it which you can checkout at [https://github.com/y-a-v-a/claude-cude-custom-commands](https://github.com/y-a-v-a/claude-cude-custom-commands). The next step is to use the VERSION file to trigger my GitHub Actions workflows for automated deployments and releases.

At approximately 2.2k tokens per execution, this command is remarkably cost-effective compared to the time and potential errors it saves.

## Beyond Version Management

Since discovering this feature, I've created several other custom commands:

- `/project:y-update-readme` - Analyses repo and some commits to update your `README.md`
- `/project:y-giti` - Initializes a Git repository, adds a `.gitignore` with some basic file mentions and commits `.gitignore`
- `/project:y-attribution` - Adds a formatted attribution text at the bottom of a project's `README.md`

Each command encapsulates domain knowledge and best practices, making our team more efficient and consistent.

## Getting Started

Creating your own custom commands is straightforward:

1. Create a `.claude/commands` directory in your project
2. Add a Markdown file for each command (filename becomes the command name)
3. Use `$ARGUMENTS` for dynamic inputs
4. Invoke with `/project:command-name arguments`

## Conclusion

If you're still manually managing versions, deployments, or any other routine tasks, I highly recommend exploring custom commands. The initial investment in creating them pays off in reduced errors, improved consistency, and freed-up mental space for the work that actually matters.

The development workflow automation possibilities are endless – and that's exactly what makes this feature so exciting.
