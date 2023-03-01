---
title: Productive VS Code Extensions
tags:
  - Extensions
categories:
  - VS Code
date: 2017-11-21 21:23:07
---

I have been using Visual Studio Code now for over a year and I absolutely love the productivity it is given to me working with React and Angular projects.

# List of Extensions

  1. [Angular 5 Snippets](#angular-5-snippets)
  1. [Auto Import](#auto-import)
  1. [Angular2 Inline](#angular2-inline)
  1. [Angular2 Switcher](#angular2-switcher)
  1. *[ESLint](#eslint)
  1. [TSLint](#tslint)
  1. [Angular Language Service](#angular-language-service)
  1. [Auto Rename Tags](#auto-rename-tags)
  1. *[Bracket Pair Colorizer](#bracket-pair-colorizer)
  1. [Code Spell Checker](#code-spell-checker)
  1. [Mocha sidebar](#mocha-sidebar)
  1. [Mark Jump](#mark-jump)
  1. *[Project Manager](#project-manager)
  1. *[Settings Sync](#settings-sync)
  1. *[Indent Rainbow](#indent-rainbow)
  1. *[Tabnine AI Autocomplete](#tabnine-ai-autocomplete)
  1. [Shortcuts](#shortcuts)

## [Angular 5 Snippets](https://marketplace.visualstudio.com/items?itemName=Mikael.Angular-BeastCode) <a id="angular-5-snippets"></a>

Visual Studio Code TypeScript and Html snippets and code examples for Angular 2+.

### Installation

Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.
```
ext install Mikael.Angular-BeastCode
```

## [Auto Import](https://marketplace.visualstudio.com/items?itemName=steoates.autoimport) <a id="auto-import"></a>

Automatically finds, parses and provides code actions and code completion for all available imports. Works with Typescript and TSX.

### Installation

Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.

```txt
ext install steoates.autoimport
```

## [Angular2 Inline](https://marketplace.visualstudio.com/items?itemName=natewallace.angular2-inline) <a id="angular2-inline"></a> ##
_This extension replaces the language-vscode-javascript-angular2 extension._

This package is a language extension for Microsoft Visual Studio Code. It extends the javascript and typescript languages to add Angular2 specific features for inline templates and stylesheets. When you define an inline template or inline style sheet using the backtick character(\`) the content will be processed by this extension.

The features provided by this extension:

Syntax highlighting of inline html and css.
Code completion, highlighting, and hover information for inline html.

#### Installation ####
Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.
```
ext install natewallace.angular2-inline
```

## [Angular2 Switcher](https://marketplace.visualstudio.com/items?itemName=natewallace.angular2-inline) <a id="angular2-switcher"></a>

Easily navigate to typescript(.ts)|template(.html)|style(.scss/.sass/.less/.css) in angular2 project.

#### Installation ####
Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.

```
ext install infinity1207.angular2-switcher
```

## [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint.tslint) <a id="eslint"></a>

Integrates [ESLint](http://eslint.org/) into VS Code. If you are new to ESLint check the [documentation](http://eslint.org/).

The extension uses the ESLint library installed in the opened workspace folder. If the folder doesn't provide one the extension looks for a global install version. If you haven't installed ESLint either locally or globally do so by running npm install eslint in the workspace folder for a local install or *`npm install -g eslint`* for a global install.

On new folders you might also need to create a .eslintrc configuration file. You can do this by either using the VS Code command Create ESLint configuration or by running the eslint command in a terminal. If you have installed ESLint globally (see above) then [run eslint --init](http://eslint.org/docs/user-guide/command-line-interface) in a terminal. If you have installed ESLint locally then run [.\node_modules\.bin\eslint --init](http://eslint.org/docs/user-guide/command-line-interface) under Windows and [./node_modules/.bin/eslint --init](http://eslint.org/docs/user-guide/command-line-interface) under Linux and Mac.

### Installation

Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.

```txt
ext install dbaeumer.vscode-eslint
```

## [TSLint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint) <a id="tslint"></a> ##
Integrates the [tslint](#https://github.com/palantir/tslint) linter for the TypeScript language into VS Code.

Please refer to the tslint [documentation](#https://github.com/palantir/tslint) for how to configure the linting rules.

#### Prerequisites ####
The extension requires that the tslint and typescript modules are installed either locally or globally. The extension will use the tslint module that is installed closest to the linted file. To install tslint and typescript globally you can run

```bash
npm install -g tslint typescript.
```

#### Installation ####
Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.
```
ext install infinity1207.angular2-switcher
```

## [Angular Language Service](https://marketplace.visualstudio.com/items?itemName=Angular.ng-template) <a id="angular-language-service"></a> ##
Editor services for Angular templates. When typing in inline or external templates you will get suggestions for autocompletion.

#### Installation ####
Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.
```
ext install Angular.ng-template
```

#### Using ####
This extension provides a rich editing experience for Angular templates, both inline and external templates including:

* Completions lists
* AOT Diagnostic messages
* Quick info
* Go to definition

This extension uses @angular/language-service@5.0.0-beta.5 and typescript@2.4.2.

## [Auto Rename Tags](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag) <a id="auto-rename-tags"></a> ##
Editor services for Angular templates. When typing in inline or external templates you will get suggestions for autocompletion.

If you rename an HTML tag, the related closing tag will be adjusted simultaneously.

<img src="https://raw.githubusercontent.com/formulahendry/vscode-auto-rename-tag/master/images/usage.gif" width="727" height="473" alt="Usage example" />

#### Installation ####
Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.
```
ext install formulahendry.auto-rename-tag
```

#### Configuration ####
Add entry into auto-rename-tag.activationOnLanguage to set the languages that the extension will be activated. By default, it is ["*"] and will be activated for all languages.

```json
{
    "auto-rename-tag.activationOnLanguage": [
        "html",
        "xml",
        "php",
        "javascript"
    ]
}
```

__Note__: The setting should be set with language id defined in VS Code. Taking javascript definition as an example, we need to use javascript for .js and .es6, use javascriptreact for .jsx. So, if you want to enable this extension on .js file, you need to add javascript in settings.json.

## [Bracket Pair Colorizer](https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer) <a id="bracket-pair-colorizer"></a> ##
Note: This extension has grown beyond its initial requirements and needs a rewrite for better language support.

This extension allows matching brackets to be identified with colours. The user can define which characters to match, and which colours to use.

All pairs of related brackets ( (...) , {...} , [...] , as well in nested constellations) will be colored with a specific color.

<img src="https://github.com/CoenraadS/BracketPair/raw/master/images/example.png" width="" height="" alt="Screenshot" />

#### Installation ####
Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.
```
ext install CoenraadS.bracket-pair-colorizer
```

## [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) <a id="code-spell-checker"></a> ##
A basic spell checker that works well with camelCase code.

The goal of this spell checker is to help with catching common spelling errors while keeping the number of false positives low.

#### Installation ####
Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.
```
ext install streetsidesoftware.code-spell-checker
```

#### Functionality ####
Load a TypeScript, JavaScript, Text, etc.. file. Words not in the dictionary files will have a squiggly underline.

#### Example ####
<img src="https://raw.githubusercontent.com/Jason-Rev/vscode-spell-checker/master/client/images/example.gif" width="" height="" alt="Example" />

## [Mocha sidebar](https://marketplace.visualstudio.com/items?itemName=maty.vscode-mocha-sidebar) <a id="mocha-sidebar"></a> ##
Mocha side bar is the most complete extension for mocha testing based on not maintained mocha extension and supports all of its features and much more.

#### Installation ####
Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.
```
ext install maty.vscode-mocha-sidebar
```

#### Functionality ####
Mocha side bar already supports this features:

* See all tests in vscode side bar menu
* Run tests for each level hierarchy from all tests to a single test(and each describer of course)
* Debug tests for each level hierarchy from all tests to a single test(and each describer of course)
* Auto run tests on file save
* NEW: see tests results directly on the code
* NEW:run/debug results directly from the code

#### Configuration ####
As I am using the NODE_PATH variable for the relative paths, I have to set it using the "mocha.env" option.

```json
//-------- Mocha options --------

// Mocha: Glob to search for test files
"mocha.files.glob": "test/**/**/*.js",

// Mocha: Environment variables to run your tests
"mocha.env": {
  "NODE_PATH": ".",
  "TEST_ENV": "unit",
  "NODE_ENV": "development",
},

// Mocha: Options to run Mocha
"mocha.options": {
  "timeout": 10000
},

//Mocha: this option allows you to enable/disable lens decorations and set update threshold "
"mocha.sideBarOptions": {
  "default": {
      "lens": true, // -> enable/disable lens
      "decoration": true, // -> enable/disable decoration
      "autoUpdateTime": 600000 // -> set timeout between each decorations and lens updates during test writing
  }
}
```

#### Example

<img src="https://i.imgur.com/p2yuNWl.png" width="" height="" alt="Working example" />

#### Functionality

Mocha side bar already supports this features:

* See all tests in vscode side bar menu
* Run tests for each level hierarchy from all tests to a single test(and each describer of course)
* Debug tests for each level hierarchy from all tests to a single test(and each describer of course)
* Auto run tests on file save
* NEW: see tests results directly on the code
* NEW:run/debug results directly from the code

#### Configuration

As I am using the NODE_PATH variable for the relative paths, I have to set it using the "mocha.env" option.

## [Mark Jump](https://marketplace.visualstudio.com/items?itemName=spywhere.mark-jump)<a id="mark-jump"></a>

Jump to the marked section in the code

#### Installation

Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.
```
ext install spywhere.mark-jump
```

#### What is Mark Jump?
Mark Jump is simply an extension that let you jump across your marking points in the code.

#### How to use it?

Simply install the extension, Mark Jump should show the mark count in the status bar! Use arrow keys to jump between them, click to jump to it.

You can also use the following key bindings to jump through various type of marks...

* Ctrl+Alt+P / Ctrl+Cmd+P (markJump.jumpToProjectMarks): Jump to all marks in the project
* Ctrl+Alt+M / Ctrl+Cmd+M (markJump.jumpToMarks): Jump to all marks (either in current editor or a whole project)
* Ctrl+Alt+S / Ctrl+Cmd+S (markJump.jumpToEditorMarks.section): Jump to all section marks (in current editor)
* Ctrl+Alt+T / Ctrl+Cmd+T (markJump.jumpToEditorMarks.todo): Jump to all TODOs (in current editor)
* Ctrl+Alt+N / Ctrl+Cmd+N (markJump.jumpToEditorMarks.note): Jump to all Notes (in current editor)
* Ctrl+Alt+, / Ctrl+Cmd+, (markJump.jumpToPreviousMark): Jump to previous mark (in current editor)
* Ctrl+Alt+. / Ctrl+Cmd+. (markJump.jumpToNextMark): Jump to next mark (in current editor)

## [Project Manager](https://github.com/alefragnani/vscode-project-manager) <a id="project-manager"></a>

Project Manager is an open source extension created for Visual Studio Code. While being free and open source, if you find it useful, please consider supporting it

It helps you to easily access your projects, no matter where they are located. Don't miss that important projects anymore. You can define your own Favorite projects, or choose for auto-detect VSCode projects, Git, Mercurial and SVN repositories or any folder.

Since version 8 you have a dedicated Activity Bar for your projects!

### What's new in Project Manager 9

* Moves the Treeview to its own Activity Bar
* Adds Add to Workspace command to add any project to current workspace
* Use new NotificationUI while refreshing projects

#### [Installation](https://marketplace.visualstudio.com/items?itemName=alefragnani.project-manager)

Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.
```
ext install alefragnani.project-manager
```

### Features

#### Available Commands

* Project Manager: ``Save Project`` Save the current folder as a new project
* Project Manager: ``Edit Project`` Edit your projects manually (projects.json)
* Project Manager: ``List Projects`` to Open List all saved/detected projects and pick one
* Project Manager: ``List Projects`` to Open in New Window List all saved/detected projects and pick one to be opened in New Window
* Project Manager: ``Refresh Projects`` Refresh the cached projects

### Open project in a new window (Version 9.0.0)

#### Steps

* Open settings
* Search by: projectManager.openInNewWindow
* Check option: "Project Manager: Open In New Window When Clicking In Status Bar"

## [Settings Sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync) <a id="settings-sync"></a> ##

Synchronize Settings, Snippets, Themes, File Icons, Launch, Keybindings, Workspaces and Extensions Across Multiple Machines Using GitHub Gist.

### Installation

Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.

```
ext install Shan.code-settings-sync
```

### Key Features

1. Use your GitHub account token and Gist.
1. Easy to Upload and Download on one click.
1. Show a summary page at the end with details about config and extensions effected.
1. Auto download Latest Settings on Startup.
1. Auto upload Settings on file change.
1. Share the Gist with other users and let them download your settings.
1. Supports GitHub Enterprise
1. Support pragmas with @sync keywords: host, os and env are supported.

Check the "Steps To Get a Personal Access Token from GitHub" to setup Setting Sync and a GitHub account.

## [Indent Rainbow](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow) <a id="indent-rainbow"></a> ##

This extension colorizes the indentation in front of your text, alternating four different colors on each step. Some may find it helpful in writing code for Python, Nim, Yaml, and probably even filetypes that are not indentation dependent.

### Installation

Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.

```
ext install oderwat.indent-rainbow
```

### Configuration

Although you can use it as it is, there is the possibility to configure some aspects of the extension:

```json
  // For which languages indent-rainbow should be activated (if empty it means all).
  "indentRainbow.includedLanguages": [] // for example ["nim", "nims", "python"]

  // For which languages indent-rainbow should be deactivated (if empty it means none).
  "indentRainbow.excludedLanguages": ["plaintext"]

  // The delay in ms until the editor gets updated.
  "indentRainbow.updateDelay": 100 // 10 makes it super fast but may cost more resources
```

## [Tabnine AI Autocomplete](https://marketplace.visualstudio.com/items?itemName=TabNine.tabnine-vscode) <a id="tabnine-ai-autocomplete"></a> ##

Tabnine AI Autocomplete for Javascript, Python, Typescript, PHP, Go, Java, Ruby & more. Code faster with AI code completions.

### Installation

Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.

```
ext install TabNine.tabnine-vscode
```

Check extension configuration [page](https://marketplace.visualstudio.com/items?itemName=TabNine.tabnine-vscode) for more information.

## Shortcuts <a id="shortcuts"></a>

### Lower Case and Upper Case

From Visual Studio Code version 1.8.1 or above you can customize your own shortcuts to do it .

1. Top menu: File-> Preferences -> Keyboard Shortcuts.
1. Click over keybindings.json and an editor will appear with keybindings.json file.
1. Place the following JSON in there and save.
```json
[
    {
        "key": "ctrl+k u",
        "command": "editor.action.transformToUppercase",
        "when": "editorTextFocus"
     },
     {
        "key": "ctrl+k l",
        "command": "editor.action.transformToLowercase",
        "when": "editorTextFocus"
     }
]
```

### Copy lines

Copy line down:
```json
  ...
   {
        "key": "Ctrl+Alt+Windows+Down",
        "command": "editor.action.copyLinesDownAction",
        "when": "editorTextFocus"
    },
  ...
```
Copy line up:
```json
  ...
   {
        "key": "Ctrl+Alt+Windows+Up",
        "command": "editor.action.copyLinesUpAction",
        "when": "editorTextFocus"
    },
  ...
```

### Select a line

Ctrl+i

### [Multi-cursor modifier](https://code.visualstudio.com/docs/editor/codebasics#_multicursor-modifier)

If you'd like to change the modifier key for applying multiple cursors to Cmd+Click on macOS and Ctrl+Click on Windows and Linux, you can do so with the **editor.multiCursorModifier** [setting](https://code.visualstudio.com/docs/getstarted/settings). This lets users coming from other editors such as Sublime Text or Atom continue to use the keyboard modifier they are familiar with.

The setting can be set to:

* `ctrlCmd` - Maps to ``Ctrl`` on Windows and Cmd on macOS.
* `alt` - The existing default ``Alt``.

There's also a menu item Use Ctrl+Click for Multi-Cursor in the Selection menu to quickly toggle this setting.

**I use this option because I use `Alt+Click` in GNU/Linux to move windows, I don not wat change that behaviour which I have used per years.**

```json
  // DEFAULT:
  // The modifier to be used to add multiple cursors with the mouse. `ctrlCmd` maps to `Control` on Windows and Linux and to `Command` on macOS. The Go To Definition and Open Link mouse gestures will adapt such that they do not conflict with the multicursor modifier.
  "editor.multiCursorModifier": "alt"

  ...

  // MY OPTION:
  "editor.multiCursorModifier": "ctrlCmd",
```

The Go To Definition and Open Link gestures will also respect this setting and adapt such that they do not conflict. For example, when the setting is ctrlCmd, multiple cursors can be added with `Ctrl/Cmd+Click`, and opening links or going to definition can be invoked with `Alt+Click`.

> You can also add more cursors with `Ctrl+Shift+`L, which will add a selection at each occurrence of the current selected text.

### Insert cursor at end of each line

Shift+Alt+i

<img src="https://i.stack.imgur.com/W6SRV.png" alt="Insert cursor at end of each line" />

### Trim Trailing Whitespace

You can enable whitespace trimming from settings:

1. Open VS User Settings (Preferences > User Settings). This will open two side-by-side documents.
2. Add a new "files.trimTrailingWhitespace": true setting to the User Settings document on the right if it's not already there. This is so you aren't editing the Default Setting directly, but instead adding to it.
3. Save the User Settings file.

### Basic Editing

Visual Studio Code is an editor first and foremost and includes the features you need for highly productive source code editing. This topic takes you through the basics of the editor and helps you get moving with your code.

* https://code.visualstudio.com/docs/editor/codebasics
* https://code.visualstudio.com/docs/getstarted/keybindings

### Official VSCode Keyboard shortcut cheatsheets:

* https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf
* https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf
* https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf
