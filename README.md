# CoolLab Devlog

See the website at : https://coollibs.github.io/CoolLab-Devlog/

How to edit the website :

## Install Hugo

We use a static site generator called Hugo. Download it here : https://gohugo.io/getting-started/installing

## Run the development server

Open a terminal at the root of this repo and run
```
hugo server
```
It will serve the website at http://localhost:1313/CoolLab-Devlog/

## Write an article

Run
```
hugo new content/post/my-article.md
```

You can now open the newly created *content/post/my-article.md* file and start writing.

You will find an overview of the markdown syntax [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet), and a list of all the additional commands [here](https://themes.gohugo.io//theme/cupper-hugo-theme/cupper-shortcodes/).

We use this theme :  https://github.com/zwbetz-gh/cupper-hugo-theme ; you might find some useful information there.

## Customize the frontmatter

The frontmatter is the area where you define metadatas and parameters for your article (it is delimited by *---* at the top of your file).

### author

If you haven't been added already, go to *layouts/post/single.html* and add a block like this :
```
{{ if eq .Params.author "jules" }}
      <a href="https://julesfouchy.github.io/home/">Jules Fouchy</a>
{{ end }}
```

### toc

Enable or disable the table of content.

### draft

Hides your article when set to true.

## Deploy your changes

Simply push them on GitHub and the site will be updated automatically.
This also means that you should be mindful of what you push. If you don't want you article to appear just yet, you can set
```
draft: true
```
in the frontmatter.