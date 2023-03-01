---
title: Getting started with Hexo
tag: Hexo
category: Hexo
---
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Quick Start

### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Setup deployment to github

Install the hexo-deployer-git module using NPM and add the following bits of configuration to your `_config.yml` file to set it up:

#### Installation
``` bash
$ npm install hexo-deployer-git --save
```

#### Options
``` yml
deploy:
  type: git
  repo: https://github.com/yourusername/your-blog-url.github.io.git
  branch: master
  message: Default to Site updated {{ now('YYYY-MM-DD HH:mm:ss') }}
```

Replace the [username] bits with your username and save the configuration. `your-blog-url.github.io.git` has to be created previously into GitHub.
Now you can run the following set of commands to generate and deploy your website:

### Generate static files
Generate Markdown to HTML.

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

### Just create a common npm script.
You can create a script in `package.json` file including above commands in one.

``` json
"scripts": {
  "deploy": "hexo generate && hexo deploy",
  "watch": "hexo server --draft --open"
}
```

More info: [Deployment](https://hexo.io/docs/deployment.html)

### Using a custom Domain (CNAME).
To use a custom domain for your Hexo website, e.g. blog.pablomagro.co.nz
 instead of pablomagro.github.io, then you need to create a file named **CNAME** to the hexo project source directory

``` bash
   source/CNAME
   blog.pablomagro.co.nz
```

You will need to own this custom domain and set your domain to point to the actual web address.

For example:

![GoDaddy Hosting](https://c1.staticflickr.com/9/8292/29032060104_be33416b81_o.png)

## Enabling Disqus Comments

### Register for a Disqus Account

In order to setup Disqus on your Hexo site you must first create a Disqus account by registering at the following link: https://disqus.com/profile/signup/.

Reed more from the following [link][1].

---

## Install additional plugins

### hexo-renderer-marked

The hexo marked renderer is a markdown rendering engine that enables you to configure how your markdown should be processed. The module follows commonmark specs as much as possible.

More info: [Rendered Marked](https://github.com/hexojs/hexo-renderer-marked)

#### Installation
``` bash
$ npm install hexo-renderer-marked --save
```

#### Options
You can configure this plugin in `_config.yml`.
``` yaml
# Marked renderer
marked:
  gfm: true
  pedantic: false
  sanitize: false
  tables: true
  breaks: false
  smartLists: true
  smartypants: true
```

### hexo-generator-category
If you like, you can include a page for every category you use on your weblog. Add a property to your markdown files that specify in which category the post belongs and install this module to generate a page for that category.
```
---
title: youtube-dl
tags: youtube-dl
categories: CLI
date: 2016-09-13 16:13:19
---
```

#### Installation
``` bash
$ npm install hexo-generator-category --save
```

#### Options
You can configure this plugin in `_config.yml`.
``` yaml
category_generator:
  per_page: 10
```

### hexo-generator-tag
You can select a tag and go to a page listing all the posts that are tagged with that particular tag. The hexo-generator-tag module is required for this functionality, so I suggest you install this if you like to enable people to browse your site by tag.

#### Installation
``` bash
$ npm install hexo-generator-tag --save
```

#### Options
You can configure this plugin in `_config.yml`.
``` yaml
tag_generator:
  per_page: 10
```

<!---
### hexo-generator-cname
You can use a custom domain name for your github pages website. All you need to do is add a CNAME file with your custom domainname in it and link the Github IP-Address in your DNS registration to your domainname.

#### Installation
``` bash
$ npm install hexo-generator-cname --save
```

#### Enable
Add hexo-generator-cname to plugins in `_config.yml`.
``` yaml
plugins:
  - hexo-generator-cname
```
-->

### hexo-generator-feed
Feed generator for Hexo

#### Installation
``` bash
$ npm install hexo-generator-feed --save
```

#### Options
You can configure this plugin in `_config.yml`.
``` yaml
feed:
  type: atom
  path: atom.xml
  limit: 20
  hub:
```

- **type** - Feed type. (atom/rss2)
- **path** - Feed path. (Default: atom.xml/rss2.xml)
- **limit** - Maximum number of posts in the feed (Use `0` or `false` to show all posts)
- **hub** - URL of the PubSubHubbub hubs (Leave it empty if you don't use it)

[1]: http://dddotcom.github.io/2014/12/28/enabling-disqus-comments/
