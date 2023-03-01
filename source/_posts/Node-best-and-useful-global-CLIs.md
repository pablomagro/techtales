---
title: Node best and useful global CLIs
date: 2018-08-24 07:54:18
tags:
  - Node
categories:
  - Global
---

# General utilities

Use sudo if you are using GNU/Linux

```bash
npm install -g tldr
npm install -g fkill-cli

```

## tldr

A Node.js based command-line client for [tldr](https://github.com/tldr-pages/tldr).

### Usage

To see tldr pages:

```
tldr --update download the latest pages and generate search index
```

### Example

Find the tldr page for the `find` command.

```
$ tldr find

  find

  Find files under the given directory tree, recursively.

  - Find files by extension:
    find root_path -name '*.ext'

  - Find files matching path pattern:
    find root_path -path '**/lib/**/*.ext'

  - Run a command for each file, use {} within the command to access the filename:
    find root_path -name '*.ext' -exec wc -l {} \;

  - Find files modified in the last 24-hour period:
    find root_path -mtime -1

  - Find files using case insensitive name matching, of a certain size:
    find root_path -size +500k -size -10MB -iname '*.TaR.gZ'

  - Delete files by name, older than 180 days:
    find root_path -name '*.ext' -mtime +180 -delete

  - Find files matching more than one search criteria:
    find root_path -name '*.py' -or -name '*.r'

  - Find files matching a given pattern, while excluding specific paths:
    find root_path -name '*.py' -not -path '*/site-packages/*'
```

## [fkill-cli](https://www.npmjs.com/package/fkill-cli)

Fabulously kill processes. Cross-platform.

Sometimes you know the process you want to finish and then you do not need to type: ``ps -ef | grep -i <process-name>``, then can use th interactive fkill-cli and select the process to kill.

### Usage

```bash
$ fkill --help

Usage
  $ fkill [<pid|name> …]

Options
  --force -f    Force kill
  --verbose -v  Show process arguments

Examples
  $ fkill 1337
  $ fkill safari
  $ fkill :8080
  $ fkill 1337 safari :8080
  $ fkill

To kill a port, prefix it with a colon. For example: :8080.

Run without arguments to use the interactive interface.
The process name is case insensitive.
```
