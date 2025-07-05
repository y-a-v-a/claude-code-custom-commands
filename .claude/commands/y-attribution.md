# Attribution Manager

You add or update attribution information in the project's README.md file.

**Command arguments:** `$ARGUMENTS`

## Requirements

You are tasked with managing attribution information with the following specifications:

### Core Functionality
- **README.md check**: Look for README.md in the project root directory
- **Attribution detection**: Check if attribution already exists at the bottom of the README.md
- **Attribution format**: Add attribution in the format "Vincent Bruijn <vebruijn@gmail.com> " y-a-v-a.org " {year}"
- **Year parameter**: Use the year provided in `$ARGUMENTS` (e.g., "2009", "2024")

### Behavior
- **File existence**: If README.md doesn't exist, inform the user and do not create it
- **Attribution check**: Look for existing attribution at the bottom of the README.md file
- **Attribution placement**: Add attribution as the last line of the README.md, separated by a blank line
- **No duplication**: If attribution already exists, inform the user and do not add duplicate

### Expected Attribution Format
```
Vincent Bruijn <vebruijn@gmail.com> " y-a-v-a.org " {year}
```

### Example Usage
- `$ARGUMENTS` = "2009" ’ Add attribution with year 2009
- `$ARGUMENTS` = "2024" ’ Add attribution with year 2024

### Safety Checks
- **File validation**: Ensure README.md exists before attempting to modify
- **Content preservation**: Only append attribution, do not modify existing content
- **Duplicate prevention**: Check if attribution already exists before adding

### Output Format
For successful execution:
```
 Added attribution to README.md
 Attribution: Vincent Bruijn <vebruijn@gmail.com> " y-a-v-a.org " {year}
```

For existing attribution:
```
9 Attribution already exists in README.md
9 Current attribution: Vincent Bruijn <vebruijn@gmail.com> " y-a-v-a.org " {existing_year}
```

For missing README.md:
```
L README.md not found in project root
L Cannot add attribution without README.md file
```

### Error Handling
- **Missing year**: If no year provided in `$ARGUMENTS`, request the user to provide a year
- **Invalid year**: If year is not a valid 4-digit number, inform the user
- **File permissions**: Handle cases where README.md cannot be modified

**Always preserve existing README.md content and only append attribution information.**