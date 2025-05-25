# README Update Command

Automatically update the README.md file based on recent repository changes and project structure.

**Command arguments:** `$ARGUMENTS`

## Requirements

You are tasked with updating or creating the README.md file with the following specifications:

### Core Functionality
- **README creation**: If README.md doesn't exist, create it with proper project structure
- **Content analysis**: Analyze recent git commits, file structure, and existing documentation
- **Intelligent updates**: Update relevant sections based on repository changes
- **Preserve existing content**: Maintain manually written content while updating generated sections

### Analysis Scope
- **Recent commits**: Review last 10-20 commits for significant changes
- **File structure**: Analyze directory structure and key files (package.json, Cargo.toml, etc.)
- **Documentation files**: Check for existing docs, changelog, or other README files
- **Code patterns**: Identify main technologies, frameworks, and project type

### README Sections to Include/Update
- **Project title and description**: Based on repository name and code analysis
- **Installation instructions**: Detect package managers and dependencies
- **Usage examples**: Generate examples based on entry points and main functionality
- **API documentation**: Extract from code comments or existing docs
- **Contributing guidelines**: Standard guidelines unless project-specific ones exist
- **License information**: Detect from LICENSE file or package.json
- **Requirements/Dependencies**: List runtime and development dependencies

### Special Features
- **Custom instructions**: Use `$ARGUMENTS` for additional update requirements
- **Version awareness**: Include current version from VERSION file if present
- **Technology detection**: Automatically detect and document tech stack
- **Link validation**: Ensure internal links work and external links are valid
- **Markdown**: Always use Markodown

### Content Preservation
- **Manual sections**: Preserve hand-written content and custom sections
- **Merge strategy**: Intelligently merge new content with existing README.md
- **Backup approach**: Show what would be changed before applying updates

### Examples of Custom Instructions
- `"update copyright information"` - Update copyright year and holder
- `"add API documentation section"` - Generate API docs from code
- `"include deployment instructions"` - Add deployment guidance
- `"update dependencies list"` - Refresh dependency information
- `"add troubleshooting section"` - Include common issues and solutions

### Output Format
Show what changes would be made:
```
📋 README Analysis:
- Project type: Node.js/TypeScript project
- Last updated: 3 months ago
- Missing sections: API documentation, troubleshooting

🔄 Planned Updates:
- Update dependencies list (5 new packages added)
- Add API documentation section
- Refresh installation instructions
- Update copyright year to 2025

✅ README.md updated successfully
```

### Error Handling
Handle these scenarios gracefully:
- No git history available
- Unreadable file permissions
- Merge conflicts with existing content
- Missing dependency files
- Invalid README.md format

### Safety Checks
- **Backup existing README.md**: Always preserve original content
- **Incremental updates**: Make targeted changes rather than complete rewrites
- **Content validation**: Ensure generated content is accurate and helpful
- **Link verification**: Validate that generated links and references work

**Always maintain professional documentation standards and ensure the README.md accurately reflects the current state of the project.**
**Do not create any files other than README.md if not present**