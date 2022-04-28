# Embed-Markdown User Guide <!-- omit in toc -->
Embed-Markdown embeds code snippets into Markdown files. It helps keep examples
up to date by syncing code referenced in Markdown files with your actual source
code. This also makes it easier to ensure samples are unit tested, etc. Snippets
can be extracted from any text file (not necessarily even a from a code file).

## Topics <!-- omit in toc -->
- [Installation](#installation)
- [Quick Start](#quick-start)
  - [Source Code References](#source-code-references)
    - [`relative_script_path`](#relative_script_path)
    - [`cmd`](#cmd)
    - [1) by **Scope**](#1-by-scope)
    - [2) by **Section**](#2-by-section)
  - [Remove Embedded Source Code](#remove-embedded-source-code)

# Installation
1. Run `pip install embed-markdown`
2. Make sure `embed-markdown` is in the 'PATH'
   1. Run `pip show embed-markdown` to show where it's installed
   2. Edit `~/.bash_profile` (or equivalence of it) to include the path
   3. Run `source ~/.bash_profile`

# Quick Start
To use this tool, first add source code references to your Markdown files. Then
run `embed-markdown` to update all Markdown files inside the
current directory (and all subdirectories) with the latest source code
referenced.

## Source Code References
Source code is embedded using a comment in your Markdown file like this:

    <!-- embed:relative_script_path:cmd:args -->

```diff
- CAUTION: This should be placed on a line by itself to avoid losing data. Do
- not modify embedded code directly because changes will be overwritten the
- next time the script runs; instead, change the source code the embed
- directive references.
```

### `relative_script_path`
This is the relative path from the *.md* file to a source file, e.g.
*../src/api.js*.

### `cmd`
This controls how a source code snippet is selected. There are two approaches:

### 1) by **Scope**
When `cmd` is "scope", embed-md will extract the next code block (inside a pair
of "{" and "}"). In this mode, `args` is a colon separated list of nested
scopes. The script scans through the target script and recursively narrows down
on each scope. When the innermost scope is found, the script extracts lines
until the next block scope ends (a complete pair of "{" and "}"). For example,
`<!-- embed:../src/api.js:scope:class SomeApi -->` extracts

    class SomeApi {
        // Some comments
        method (a) {
            if (a) {
                console.log(a)
            }
        }
    }

Whereas `<!-- embed:../src/api.js:scope:class SomeApi:Some comments -->`
extracts

    // Some comments
    method (a) {
        if (a) {
            console.log(a)
        }
    }

And `<!-- embed:../src/api.js:scope:class SomeApi:Some comments:if (a) -->`
extracts

    if (a) {
        console.log(a)
    }

### 2) by **Section**
When `cmd` is "section", embed-md will extract lines between the section start
and end patterns. In this mode, `args` is two colon delimited strings with
pattern `start_pattern:end_pattern`. Code between lines with substring
`start_pattern` and `end_pattern` are extracted from the target script. For
example, `<!-- embed:../example.js:section:Example 1 start:Example 1 end -->`
extracts

    const a = 1

from

    // Example 1 start
    const a = 1
    // Example 1 end

## Remove Embedded Source Code
Run `embed-markdown --remove` to remove all embedded code snippets, leaving only
the embed directive.
