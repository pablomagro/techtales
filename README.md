# Setup

Get the application code cloning the git repository and installing all the dependencies.

```bash
$ git clone https://pablomagro@bitbucket.org/mydevelopments/pablomagro.github.io.git
$ cd pablomagro.github.io
$ npm install
```

## Pull up the server (devolopment).

```bash
$ npm run watch
```

## Deploy on Production.

```bash
$ npm run deploy
```

# Actions

## Create a new blog entry

Create a new git branch and then create the new blog entry.

```bash
git checkout -b <branch-name> && hexo new <'branch name'>
```

# Documentation

1. [actions-gh-pages](https://github.com/peaceiris/actions-gh-pages#%EF%B8%8F-allow-empty-commits-allow_empty_commit)
