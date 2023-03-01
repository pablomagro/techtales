---
title: Post Installing GNU/Linux (Debian based)
tags:
  - Install
  - Post Install
categories:
  - GNU/Linux
  - Debian
date: 2016-09-18 10:21:11
---

## 0. Debian [Backports](https://backports.debian.org)

Backports are recompiled packages from testing (mostly) and unstable (in a few cases only, e.g. security updates) in a stable environment so that they will run without new libraries (whenever it is possible) on a Debian stable distribution

Backports cannot be tested as extensively as Debian stable, and backports are provided on an as-is basis, with risk of incompatibilities with other components in Debian stable. Use with care!

It is therefore recommended to select single backported packages that fit your needs, and not use all available backports.

### Add backports to your sources.list

1. For **stretch** (at the present moment) add this line:

```shell
deb http://ftp.debian.org/debian stretch-backports main
```

2. Run **apt update**.

### Install a package from backports

All backports are deactivated by default (i.e. the packages are pinned to 100 by using ButAutomaticUpgrades: yes in the Release files. If you want to install something from backports run (you can use aptitude too):

```shell
sudo apt -t stretch-backports install "package"
```

## 1. Add [multimedia][deb-multimedia] repos

After you have added the necessary line in /etc/apt/sources.list (as below)

```bash
deb ftp://ftp.deb-multimedia.org stable main non-free
```

the first package to install is deb-multimedia-keyring.

```bash
sudo apt update && apt install -y deb-multimedia-keyring
```

## 2. Update the operating system

```bash
sudo apt update && time sudo apt dist-upgrade
```

## 3. Install sudo and set permissions

As root execute below commands.

``` bash
# apt install -y sudo
# adduser user sudo
```

## 4. Installer for Microsoft TrueType core fonts

``` bash
sudo apt install ttf-mscorefonts-installer
```

### More ways to install fonts

Sometimes you download .ttf file (a font file) and you want to install it directly. In that case, copy the font file to one of the following directory.

The fonts can be copied in one of this directories:

    /usr/share/fonts
    /usr/share/X11/fonts
    /usr/local/share/fonts
    ~/.fonts

Here’s how the directories work.

If you want the fonts for everyone on the system (i.e. in a multiuser environment) then put them on /usr/share/fonts.

If you only want the fonts for yourself, then put them on ~/.fonts/ directory of your home folder.

Once you’ve copied the files in correct places, issue the following command to which will read and cache all installed fonts from these directories.

``` bash
# fc-cache -fv
```

Now if you want to list all installed and cached fonts on your system, you need to use fc-list command.

Sample output below:

``` bash
# fc-list

usr/share/fonts/truetype/msttcorefonts/comicbd.ttf: Comic Sans MS:style=Bold,Negreta,tučné,fed,Fett,Έντονα,Negrita,Lihavoitu,Gras,Félkövér,Grassetto,Vet,Halvfet,Pogrubiony,Negrito,Полужирный,Fet,Kalın,Krepko,Lodia
/usr/share/fonts/truetype/oxygen/OxygenMono-Regular.ttf: Oxygen Mono:style=Regular
/usr/share/fonts/truetype/tlwg/TlwgTypo-Bold.ttf: Tlwg Typo:style=Bold
/usr/share/fonts/truetype/dejavu/DejaVuSerif-Bold.ttf: DejaVu Serif:style=Bold
/usr/share/fonts/truetype/noto/NotoSansThai-Regular.ttf: Noto Sans Thai:style=Regular
/usr/share/fonts/truetype/fonts-kalapi/Kalapi.ttf: Kalapi:style=Regular
/usr/share/fonts/truetype/fonts-gujr-extra/Rekha.ttf: Rekha:style=Medium
/usr/share/fonts/truetype/tlwg/TlwgTypewriter-BoldOblique.ttf: Tlwg Typewriter:style=Bold Oblique
/usr/share/fonts/truetype/dejavu/DejaVuSansMono.ttf: DejaVu Sans Mono:style=Book
/usr/share/fonts/truetype/noto/NotoSansCypriot-Regular.ttf: Noto Sans Cypriot:style=Regular
/usr/share/fonts/truetype/msttcorefonts/comic.ttf: Comic Sans MS:style=Regular,Normal,obyčejné,Standard,Κανονικά,Normaali,Normál,Normale,Standaard,Normalny,Обычный,Normálne,Navadno,Arrunta
/usr/share/fonts/truetype/noto/NotoSansTeluguUI-Bold.ttf: Noto Sans Telugu UI:style=Bold
...
```

### Configuring Fonts on Linux ###

``` bash
# dpkg-reconfigure fontconfig-config
```

## 5. Install the “good stuff” such as unrar, smplayer, etc

Keep in mind I am using debian based distro and KDE, for instance some packages names don't be able to fix with your current distro.

```bash
sudo apt install unrar rar vlc smplayer mplayer curl vim mesa-utils htop lm-sensors screen kde-config-touchpad sysv-rc-conf transmission subtitleeditor pavucontrol gthumb tree
```

### Browsers

* **chromium** - the web browser from Google

```sh
sudo apt install chromium chromium-l10n
```

* **Brave**

[Installing](https://brave-browser.readthedocs.io/en/latest/installing-brave.html#release-channel-installation) brave Debian 9+, Ubuntu 14.04+ and Mint 17+

If you get `gnutls_handshake()` errors after adding the Brave repository on Debian 9, you may need to [uninstall old conflicting packages](https://github.com/signalapp/Signal-Desktop/issues/2483#issuecomment-401047201).

```sh
sudo apt install apt-transport-https curl

curl -s https://brave-browser-apt-release.s3.brave.com/brave-core.asc | sudo apt-key --keyring /etc/apt/trusted.gpg.d/brave-browser-release.gpg add -

echo "deb [arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main" | sudo tee /etc/apt/sources.list.d/brave-browser-release.list

sudo apt update

sudo apt install brave-browser
```

## 6. Installing [Git](http://rogerdudler.github.io/git-guide/) on GNU/Linux

If you want to install the basic Git tools on Linux via a binary installer, you can generally do so through the basic package-management tool that comes with your distribution.

If you’re on a Debian-based distribution like Ubuntu, try apt:

```bash
sudo apt install -y git git-flow
```

And then run to setup the default email, name and editor:

```bash
  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"
  git config --global core.editor vim
```

### PS + Git (Current branch)

Add below code into your ~/.bash before the line `unset color_prompt force_color_prompt` to see your current git branch into the bash prompt. Idea taken from [here](https://gist.github.com/justintv/168835).

```bash
# Add git branch if its present to PS1.
# parse_git_branch() {
#   git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
# }
# PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[0;37m\]\w\[\033[01;31m\] $(parse_git_branch)\[\033[00m\]\$ '
PS1='\[\033[0;32m\]\[\033[0m\033[0;32m\]\u\[\033[0;36m\] @ \[\033[0;36m\]\h \w\[\033[0;32m\]$(__git_ps1)\n\[\033[0;32m\]└─\[\033[0m\033[0;32m\] \$\[\033[0m\033[0;32m\] ▶\[\033[0m\] '
unset color_prompt force_color_prompt
```

### Productive aliases

#### Common aliases

FILE: **~/.gitconfig**
```
[user]
  email = your@email.com
  name = Your Name
[core]
  editor = vim
[merge]
  ff = false
  ff = false
[alias]
  co = checkout
  cob = checkout -b
  ci = commit
  st = status
  br = branch
  hist = log --pretty=format:\"%h %ad | %s%d [%an]\" --graph --date=short
  type = cat-file -t
  dump = cat-file -p
  branch-merged = "!git branch -r --merged | egrep -v 'master|develop' | sed 's/origin\\///g'"
  branch-cleanup = "!git branch -r --merged | egrep -v 'master|develop' | sed 's/origin\\///g' | xargs -n 1 git push --delete origin"
  lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --branches
  plr = pull --rebase
  push-release = "!git push origin `git rev-parse --abbrev-ref HEAD` && git push --tags"
```

#### Command aliases (optional)

FILES: either **~/.profile** or **~/.bashrc**

```bash
alias git_diff_commit='git whatchanged -m -n 1 -p $1'
alias git_reset='git reset --hard'
alias git_delete_remote_branch='git push origin --delete $1'
# Change commit comment.
#git commit --amend --no-verify
alias git_pull_current_branch='git fetch --all --prune && git pull origin `git rev-parse --abbrev-ref HEAD`'
alias git_push_current_branch='git push origin `git rev-parse --abbrev-ref HEAD`'
alias git_branch_merged="git branch -r --merged | egrep -v \"master|develop\" | sed 's/origin\///'"
alias git_branch_cleanup="git branch -r --merged | egrep -v \"master|develop\" | sed 's/origin\///' | xargs -n 1 git push --delete origin"
alias git_patch_export_current='current=$(git branch --show-current | sed -r "s/\//-/g") ; git format-patch -k --stdout HEAD^ > ../"$current".patch'
alias git_patch_import_current='git am -3 -k --ignore-whitespace "$1"'

# More aliases
alias g='git'
alias gs='git status '
alias ga='git add '
alias gb='git branch '
alias gc='git commit'
alias gd='git diff'
alias go='git checkout '
alias gl='git log '
alias glp='git log -p'
alias glo='git log --pretty=oneline'
alias gps='git_push_current_branch'
alias gpsr='git_push_current_branch && git push --tags'
alias gpl='git_pull_current_branch'
alias gplr='git pull --rebase'
alias gk='gitk --all&'
alias gfi='git flow init -d'

# With git reflog check which commit is one prior the merge.
alias gum='git reset --hard HEAD~1'
alias got='git '
alias get='git '
```

The `go` abbreviation for `git checkout` is very useful, allowing me to type:

```bash
go <branch>
```

to checkout a particular branch. Also, I often mistype `git` as `get` or `got` so I created aliases for them too.

### Source

* https://githowto.com/aliases

## 7. Install [screen][screen]

```bash
apt install -y screen
```

## 8. Install [Node.js][nodejs]

From [this repository](https://github.com/nodesource/distributions/blob/master/README.md#deb) contains documentation for using the NodeSource Node.js Binary Distributions via .rpm, .deb and Snap packages as well as their setup and support scripts.

~~For Node.js 8:~~
```bash
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt install -y nodejs
```

~~Alternatively, for Node.js 9:~~ Node.js 9.x is no longer actively supported!
```bash
curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash -
sudo apt-get install -y nodejs
```

**Node.js v10.x:**
```sh
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
```
```sh
# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_10.x | bash -
apt-get install -y nodejs
```

**Node.js v12.x:**

```sh
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs
```
```sh
# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_12.x | bash -
apt-get install -y nodejs
```

**Node.js v13.x:**
```sh
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_13.x | sudo -E bash -
sudo apt-get install -y nodejs
```
```sh
# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_13.x | bash -
apt-get install -y nodejs
```

### 8.1 [Node Version Manager](https://github.com/nvm-sh/nvm#installing-and-updating)

POSIX-compliant bash script to manage multiple active node.js versions

#### Install & Update Script

To **install** or **update** nvm, you should run the [install script][2]. To do that, you may either download and run the script manually, or use the following cURL or Wget command:
```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```
```sh
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```

Running either of the above commands downloads a script and runs it. The script clones the nvm repository to `~/.nvm`, and attempts to add the source lines from the snippet below to the correct profile file (`~/.bash_profile`, `~/.zshrc`, `~/.profile`, or `~/.bashrc`).

<a id="profile_snippet"></a>
```sh
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

### 8.2 [Node Task List](https://github.com/ruyadorno/ntl)
Interactive cli to list and run package.json scripts.

Install in debian (or based on):

```sh
sudo npm install -g ntl
```

## 9. Editors

## Install vim

``` bash
sudo apt install -y vim
```

And then edit the file */etc/vim/vimrc* to enable syntax highlighting.

## Installing [Atom](https://atom.io/) on GNU/Linux

Currently only a 64-bit version is available.

1. Download atom-amd64.deb from the Atom releases [page](https://github.com/atom/atom/releases/tag/v1.10.2).

 Run `sudo dpkg --install atom-amd64.deb` on the downloaded package.

3. Launch Atom using the installed atom command.

The Linux version does not currently automatically update so you will need to repeat these steps to upgrade to future releases.

You can read more informatoin in the Atom [website](https://github.com/atom/atom).

## Install [Visual Studio Code](https://code.visualstudio.com/) ##

I use the repo to keep it update along the debian updates. The repository and key can also be installed manually with the following script:

```bash
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
```

Then update the package cache and install the package using:

```bash
sudo apt update && sudo apt install -y code
```

## Install [Sublime 3](https://www.sublimetext.com)

Browser until the following URL https://www.sublimetext.com/3 and select your OS and arch or linux [repos](https://www.sublimetext.com/docs/3/linux_repositories.html) to download Sublime 3.

I have chosen the linux repos to install it. Install the GPG key:

```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
```

Ensure apt is set up to work with https sources:
```bash
sudo apt install apt-transport-https
```

Select the channel to use (stable):
```bash
sudo echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
```

Update apt sources and install Sublime Text
```bash
sudo apt update
sudo apt install sublime-text
```

### [PlainTasks](https://github.com/aziz/PlainTasks) Plugin

An opinionated todo-list plugin for Sublime Text editor (version 2 and 3)

#### Installation
To install this plugin, you have two options:

1. If you have Package Control installed, simply search for PlainTasks to install.
1. Clone source code to Sublime Text packages folder.

### Sources
* https://www.sublimetext.com/docs/3/linux_repositories.html#apt
* https://github.com/aziz/PlainTasks

## 12. SQL

### Clients Installation

**PostgreSQL**
```bash
sudo apt install -y postgresql-client
```

Some configuration for the PostgreSQL interactive terminal - psql.12. SQL

Edit the ``~/.psqlrc`` file as below:

```sql
\set AUTOCOMMIT off

-- \set PROMPT1 '%~%--%x '
-- Use table format (with headers across the top) by default, but switch to
-- expanded table format when there's a lot of data, which makes it much easier to read.
\x auto
-- \set ON_ERROR_STOP on
-- \set ON_ERROR_ROLLBACK interactive
-- Use a separate history file per-database.
--\set HISTFILE ~/.psql_history- :DBNAME
-- If a command is run more than once in a row, only store it once in the history.
\set HISTCONTROL ignoredups
-- Autocomplete keywords (like SELECT) in upper-case, even if you started
-- typing them in lower case.
\set COMP_KEYWORD_CASE upper

-- Verbose error reports.
\set VERBOSITY verbose

-- By default, NULL displays as an empty space. Is it actually an empty
-- string, or is it null? This makes that distinction visible.
--\pset null '[NULL]'
\pset null '¤'
\pset linestyle 'unicode'

\pset unicode_border_linestyle single
\pset unicode_column_linestyle single
\pset unicode_header_linestyle double

set intervalstyle to 'postgres_verbose';

\setenv LESS '-iMFXSx4R'
\setenv EDITOR '/usr/bin/vim'
```

* Link reference: https://thoughtbot.com/blog/improving-the-command-line-postgres-experience.

**[dbeaver](http://dbeaver.io)**
Free universal database tool and SQL client. It can be downloaded and installed from this [link](https://dbeaver.io/download/).

### Aministration

**PostgreSQL**
pgAdmin III is a handy GUI for PostgreSQL, it is essential to beginners. To install it, type at the command line:
```bash
sudo apt install -y pgadmin3
```

## 13. Install compressing packages

```bash
sudo apt install -y p7zip p7zip-full unrar-free unzip
```

## 14. Multimedia

* **amarok** - Easy to use media player based on the KDE Platform.
* **smplayer** - Complete front-end for MPlayer and mpv.
* **vlc** - Multimedia player and streamer.
* **soundconverter** - GNOME application to convert audio files into other formats.

```bash
sudo apt install -y mplayer smplayer vlc amarok soundconverter
```

## 15. Install shutter

Feature-rich screenshot program
```bash
sudo apt install -y shutter
```

## 16. Monitoring and networking

* **aptitude** - Terminal-based package manager.
* **intel-microcode** - Processor microcode [firmware](https://wiki.debian.org/Microcode) for Intel CPUs.
* **lm-sensors** - Utilities to read temperature/voltage/fan sensors.
* **neofetch** - Shows Linux System Information with Distribution Logo.
* **qapt-deb-installer** - tool for installing deb files.
* **net-tools** - NET-3 networking toolkit.
* **inxi** - full featured system information script

```bash
sudo apt install -y faketime htop lshw inxi pdftk wget curl net-tools filezilla neofetch qapt-deb-installer aptitude intel-microcode lm-sensors
```

Use examples:

```sh
sudo netstat -lnpt | grep Plex

inxi -Fxz
```

## 17. Audit the system

[Lynis][Lynis]: an open source tool that performs a local security assessment and audits local services for vulnerabilities. It is light-weight and easy to use; just unzip it and run the command

### Import key

```bash
wget -O - http://packages.cisofy.com/keys/cisofy-software-public.key | apt-key add -
```

### Add software repository

Using your software in English? Then configure APT to skip downloading translations. This saves bandwidth and prevents additional load on the repository servers.

```bash
echo 'Acquire::Languages "none";' > /etc/apt/apt.conf.d/99disable-translations
```

### Adding the repository:

```bash
echo "deb https://packages.cisofy.com/community/lynis/deb/ stretch main" > /etc/apt/sources.list.d/cisofy-lynis.list
```

### Install Lynis

```bash
apt update && apt install -y lynis
```

### Run the report

```bash
lynis audit system
```

## 18. Download and install Heroku CLI

This version does not autoupdate. You’ll have to manually update the cli with apt. Use the standalone install for an autoupdating version of the CLI.
Run the following to add our apt repository and install the CLI:

```bash
wget -qO- https://cli-assets.heroku.com/install-ubuntu.sh | sh

+ SUDO=
+ id -u
+ [ 1000 != 0 ]
+ SUDO=sudo
+ echo This script requires superuser access to install apt packages.
This script requires superuser access to install apt packages.
+ echo You will be prompted for your password by sudo.
You will be prompted for your password by sudo.
+ sudo -k
+ sudo sh
[sudo] password for pablo:
+ dpkg -s apt-transport-https
+ echo deb https://cli-assets.heroku.com/branches/stable/apt ./
+ dpkg -s heroku-toolbelt
+ true
+ + apt-keywget add -
 -qO- https://cli-assets.heroku.com/apt/release.key
OK
+ apt update
Ign:1 http://deb.debian.org/debian stable InRelease
Hit:2 https://repo.skype.com/deb stable InRelease
Get:3 https://cli-assets.heroku.com/branches/stable/apt ./ InRelease [2,539 B]
Hit:4 http://security.debian.org/debian-security stretch/updates InRelease
Hit:5 https://deb.nodesource.com/node_8.x stretch InRelease
Hit:6 http://deb.debian.org/debian stable-updates InRelease
Ign:7 http://dl.google.com/linux/chrome/deb stable InRelease
Get:8 https://cli-assets.heroku.com/branches/stable/apt ./ Packages [808 B]
Hit:9 http://www.deb-multimedia.org stable InRelease
Hit:10 http://deb.debian.org/debian stable Release
Hit:12 https://packages.microsoft.com/repos/vscode stable InRelease
Hit:13 http://dl.google.com/linux/chrome/deb stable Release
Hit:15 https://packages.cisofy.com/community/lynis/deb stretch InRelease
Fetched 3,347 B in 1s (2,058 B/s)
Reading package lists... Done
+ apt install -y heroku
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following NEW packages will be installed:
  heroku
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 14.2 MB of archives.
After this operation, 0 B of additional disk space will be used.
Get:1 https://cli-assets.heroku.com/branches/stable/apt ./ heroku 6.14.38-1 [14.2 MB]
Fetched 14.2 MB in 11s (1,276 kB/s)
Selecting previously unselected package heroku.
(Reading database ... 212960 files and directories currently installed.)
Preparing to unpack .../heroku_6.14.38-1_amd64.deb ...
Unpacking heroku (6.14.38-1) ...
Setting up heroku (6.14.38-1) ...
+ which heroku
+ LOCATION=/usr/bin/heroku
+ echo heroku cli installed to /usr/bin/heroku
heroku cli installed to /usr/bin/heroku
+ heroku version
heroku-cli/6.14.38-9bfc11a (linux-x64) node-v9.2.0
```

The script is easily typed in manually if you prefer not to pipe commands to sh.

### Reference

https://devcenter.heroku.com/articles/heroku-cli#debian-ubuntu

## 19. Unlimited Bash History

Something very util is go back and see how I built/configured something, or what that nifty command was, or how some command broke something weeks ago.

To archive mencioned before, Set `HISTSIZE` and `HISTFILESIZE` in `.bashrc` to an empty value. Also it makes sense not enter lines which begin with a space or tab or duplicated (such as cd ..).

```bash
HISTSIZE=
HISTFILESIZE=
HISTCONTROL=ignoreboth
```

    HISTSIZE
        The number of commands to remember in the command history (see HISTORY below). If the value is 0, commands are not saved in the history list.  Numeric  values less  than zero result in every command being saved on the history list (there is no limit). The shell sets the default value to 500 after reading any startup files.

    HISTFILESIZE
        The  maximum number of lines contained in the history file.  When this variable is assigned a value, the history file is truncated, if necessary, to contain no more than that number of lines by removing the oldest entries. The history file is also truncated to this size after writing it when a shell  exits. If  the value  is  0, the history file is truncated to zero size. Non-numeric values and numeric values less than zero inhibit truncation.  The shell sets the default value to the value of HISTSIZE after reading any startup files.

    HISTCONTROL
        A value of `ignorespace' means to not enter lines which begin with a space or tab into the history list. A value of `ignoredups' means to not enter lines which match the last entered line. A value of `ignoreboth' combines the two options. Unset, or set to any other value than those above, means to save all lines on the history list. The second and subsequent lines of a multi-line compound command are not tested, and are added to the history regardless of the value of HISTCONTROL.

### References

* Bash Variables: [http://www.faqs.org/docs/bashman/bashref_60.html](http://www.faqs.org/docs/bashman/bashref_60.html)
* man bash

## 20. Terminals

* **Yakuake** - a Quake-style terminal emulator based on KDE Konsole technology..
* **Terminator** - Multiple GNOME terminals in one window

```bash
sudo apt install yakuake terminator
```

### Terminator

Configuration file: ``~/.config/terminator/config``

Default config to open two different terminals horizonatally and executing a script:
```
[global_config]
  title_hide_sizetext = True
  enabled_plugins = LaunchpadCodeURLHandler, APTURLHandler, LaunchpadBugURLHandler
  suppress_multiple_term_dialog = True
[keybindings]
[profiles]
  [[default]]
    cursor_blink = False
    cursor_color = "#aaaaaa"
    font = DejaVu Sans Mono 9
    scrollback_infinite = True
[layouts]
  [[default]]
    [[[child0]]]
      type = Window
      parent = ""
      order = 0
      position = 960:0
      maximised = False
      fullscreen = False
      size = 956, 1015
      title = pablom@traffic-20200401: ~
      last_active_term = 074fb89a-2af2-4e50-b709-ed76bd0c9318
      last_active_window = True
    [[[child1]]]
      type = VPaned
      parent = child0
      order = 0
      position = 505
      ratio = 0.5
    [[[terminal2]]]
      type = Terminal
      parent = child1
      order = 0
      profile = default
      uuid = 074fb89a-2af2-4e50-b709-ed76bd0c9318
      command = cd ~/development/ui/control-ui/ ; bash
    [[[terminal3]]]
      type = Terminal
      parent = child1
      order = 1
      profile = default
      uuid = 0fa94cf4-db29-4f02-a4fb-af6b5a48c6da
      command = cd ~/development/rest/control-rest-service/ ; bash
```

## 21. Communication

### [Slack](https://slack.com/intl/en-nz/)
Slack brings the team together, wherever you are.

#### Slack for linux

You can download deb and rpm binaries from [here](https://slack.com/intl/en-nz/downloads/linux), and then just install it.

## Install [xclip](https://github.com/astrand/xclip)

xclip is a command line utility that is designed to run on any system with an X11 implementation.
It provides an interface to X selections ("the clipboard") from the command line.
It can read data from standard in or a file and place it in an X selection for pasting into other X applications.
xclip can also print an X selection to standard out, which can then be redirected to a file or another program.

```bash
sudo apt install xclip
# Downloads and installs xclip.

xclip -sel clip < ~/file
# Copies the contents of the file file to your clipboard.
```

## 22. Code storage

Below you can find cloud storage service providers with native Linux client.

### [Dropbox](https://www.dropbox.com/)
To install dropbox follow the next [link](https://www.dropbox.com/install-linux).

### [Mega](https://mega.nz/)

## 23. Virutalization

### [Virtualbox]((https://www.virtualbox.org))

[Download](https://www.virtualbox.org/wiki/Linux_Downloads) and install VirtualBox for Debian-based GNU/Linux hosts:

Add the following line to your /etc/apt/sources.list. According to your distribution, replace '<mydist>' with 'eoan', 'bionic', 'xenial', 'buster', 'stretch', or 'jessie' (older versions of VirtualBox supported different distributions):
```bash
sudo sh -c 'echo "deb http://download.virtualbox.org/virtualbox/debian $(lsb_release -sc) contrib" >> /etc/apt/sources.list'

# /etc/apt/sources.list:
deb http://download.virtualbox.org/virtualbox/debian buster contrib
```

The Oracle public key for apt-secure can be downloaded:
```bash
wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -
```

To install VirtualBox, do:
```bash
sudo apt update
sudo apt install virtualbox-6.1
```

Finally if you need anything of the following: Support for USB 2.0 and USB 3.0 devices, VirtualBox RDP, disk encryption, NVMe and PXE boot for Intel cards, then install the [Entension Pack](https://download.virtualbox.org/virtualbox/6.1.4/Oracle_VM_VirtualBox_Extension_Pack-6.1.4.vbox-extpack).

## 23. Miscellaneous

* **fortunes** - Data files containing fortune cookies. Configuration [here](https://wiki.debian.org/fortune).

```bash
apt install fortunes fortunes-es
```

[deb-multimedia]: http://www.deb-multimedia.org/
[screen]: https://www.gnu.org/software/screen/manual/screen.html
[nodejs]: https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions
[Lynis]: https://cisofy.com/lynis/
[baloo]: https://community.kde.org/Baloo/Configuration
