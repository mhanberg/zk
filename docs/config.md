# Configuration file

Each [notebook](notebook.md) contains a configuration file used to customize your experience with `zk`. This file is located at `.zk/config.toml` and uses the [TOML format](https://github.com/toml-lang/toml). It is composed of several optional sections:

* `[note]` sets the [note creation rules](config-note.md)
* `[extra]` contains free [user variables](config-extra.md) which can be expanded in templates
* `[group]` defines [note groups](config-group.md) with custom rules
* `[tool]` customizes interaction with external programs such as:
    * [your default editor](tool-editor.md)
    * [your default pager](tool-pager.md)
    * [`fzf`](tool-fzf.md)
* `[alias]` holds your [command aliases](config-alias.md)

## Complete example

Here's an example of a complete configuration file:

```toml
# NOTE SETTINGS
[note]

# Language used when writing notes.
# This is used to generate slugs or with date formats.
language = "en"

# The default title used for new note, if no `--title` flag is provided.
default-title = "Untitled"

# Template used to generate a note's filename, without extension.
filename = "{{id}}-{{slug title}}"

# The file extension used for the notes.
extension = "md"

# Template used to generate a note's content.
# If not an absolute path, it is relative to .zk/templates/
template = "default.md"

# Configure random ID generation.

# The charset used for random IDs.
id-charset = "alphanum"

# Length of the generated IDs.
id-length = 4

# Letter case for the random IDs.
id-case = "lower"


# EXTRA VARIABLES
[extra]
author = "Mickaël"


# GROUP OVERRIDES
[dir.journal]
paths = ["journal/weekly", "journal/daily"]

[dir.journal.note]
filename = "{{date now}}"


# EXTERNAL TOOLS
[tool]

# Default editor used to open notes.
editor = "nvim"

# Pager used to scroll through long output.
pager = "less -FIRX"

# Command used to preview a note during interactive fzf mode.
fzf-preview = "bat -p --color always {-1}"


# COMMAND ALIASES
[alias]

# Edit the last modified note.
edlast = "zk edit --limit 1 --sort modified- $@"

# Edit the notes selected interactively among the notes created the last two weeks.
recent = "zk edit --sort created- --created-after 'last two weeks' --interactive"

# Show a random note.
lucky = "zk list --quiet --format full --sort random --limit 1"
```
