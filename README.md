# Markdown Code Embed (Action)

## Contents
- [Introduction](#introduction)
- [Adding Action To Your Repository](#adding-action-to-your-repository)
- [Quick Syntax Guide](#quick-syntax-guide)
	- [Embedding Files And Contents](#embedding-files-and-contents)
	- [Embedding Process Output](#embedding-process-output)
- [More Info](#more-info)

## Introduction
This repository provides the public action for the [Markdown Code Embed](https://github.com/ippie52/markdown_code_embed/) script. Full documentation on using the script directly, with examples can be found there. 

Some examples here are taken from there with less context, however I would recommend going over to the the main repository for full documentation on how to add code to your markdown files.

This is a lightweight means of embedding live code from your repository into your markdown documentation. 

This action reports issues when it finds changes to your documentation, indicating that it may be out of date. These changes should at very least be checked to make sure that the documentation is correct, and be updated as part of the commit.

## Adding Action To Your Repository
A quick example:
```yaml:example
name: 'Update README files'

on:
  workflow_dispatch:
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      - name: Markdown Code Embed
        uses: ippie52/markdown_code_embed_action@1.0
        with: 
          args: '-s'
```
The above is embedded using this script and reflects the contents of the file [example](example). This is a fairly straight forward action, which runs a job on any pull request into the `main` branch.

The arguments provided by 
```yaml:example [17-18]
        with: 
          args: '-s'
```
are simply passed through to the `mdce.py` script, as shown below. Here, we're simply passing the `--sub` option to check through all sub-directories.

Usage of the `mdce.py` script:
```text:run:mdce.py <["-h"]>
usage: EmbedCode [-h] [-d directory [directory ...]]
                 [-f file name [file name ...]] [-s] [-b] [-g] [-u] [-q]

Embed code within markdown documents

options:
  -h, --help            show this help message and exit
  -d directory [directory ...], --directories directory [directory ...]
                        Directories to be scanned for README.md files
  -f file name [file name ...], --files file name [file name ...]
                        Files to be scanned
  -s, --sub             Checks all sub-directories
  -b, --backup          Backs up the original file, appending ".old" to the
                        file name
  -g, --ignore-git      Exit value ignores changes in git
  -u, --ignore-untracked
                        Exit value ignores changes to untracked files
  -q, --quiet           Reduces the number of messages printed
```

## Quick Syntax Guide

This guide is for the syntax within your markdown files.

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

## More Info
For more information, please head over to [the main repository](https://github.com/ippie52/markdown_code_embed/)