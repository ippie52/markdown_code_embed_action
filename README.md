# Markdown Code Embed (Action)


## Introduction
This repository provides the public action for the [Markdown Code Embed](https://github.com/ippie52/markdown_code_embed/) script. Full documentation on using the script directly can be found there. Some examples here are taken from there with less context, however I would recommend going over to the the main repository for full documentation.

## Adding Action To Your Repository
TODO

## Quick Syntax Guide

### Embedding Files And Contents

General rules:
- The opening code block must all be on one line.
- Must start with at least three back-ticks.
- Must have a language/syntax type ([here](https://github.com/jincheng9/markdown_supported_languages) is a decent list).
- Relative file name placed after the syntax, following a colon.
- Line number range, if required, in square brackets with either a colon `:` or dash `-` separating the start and end lines. A single value is also accepted.
- Must be a closing block with greater than or equal to the number of back-ticks in the opening block.

Syntax:
````markdown
```language:path/to/file [start_line-end_line]`
```
````

Example:
````markdown
``` python:mdce.py [2-6]
```
````

### Embedding Process Output

Additional rules for process captures:
- General rules above must be met
- Keyword `run` must appear after the syntax and a colon, and must be followed by a colon before the path of the file to be executed
- Arguments, if required, must be within chevrons and in JSON format (see [this section](#embed-process-output) for more details)
- Line numbers, if set, will be ignored
- Only data sent to `stdout` will be recorded. For `stderr`, a wrapper will be required.


````markdown
```language:run:path/to/file <["arg1", "arg2", "arg3"]>`
```
````

Example:
````markdown
```text:run:/usr/bin/ls <["."]>
```
````

