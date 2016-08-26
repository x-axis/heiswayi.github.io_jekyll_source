---
layout: post
title: Blog Reference Sheet
description: I am always forgetting how my blog works. 
keywords: jekyll, github, reference, quicksheet, list, latex
---

## Blog
At the core, this blog is written in [Markdown](http://daringfireball.net/projects/markdown/), which is a syntax that turns plain text into HTML. Its creator, John Gruber, sought to design a language whose syntax was "as readable as possible." Indeed, Markdown was inspired by the format of plain text email, with as few formatting tags as possible. 

The "scaffold" of this blog -- that is, the meta-programming technique that generates code from my Markdown text -- is [Jekyll](https://jekyllrb.com). From [What is Jekyll?](http://jekyllbootstrap.com/lessons/jekyll-introduction.html),

> Jekyll is a parsing engine bundled as a ruby gem used to build static websites from dynamic components such as templates, partials, liquid code, markdown, etc. Jekyll is known as "a simple, blog aware, static site generator".

Static websites do not depend on a live connection to a database or server-side code; therefore the user sees exactly what I have written at the time of publication. As a result, Jekyll only needs to parse the blog components once in order to generate a website, which is then served on a web-server. 

The web server used is [GitHub Pages](https://pages.github.com), which hosts my website from my GitHub repository. A repository is a central hub or location where things are stored - in this case, source code. As per its namesake, GitHub uses the Git version control system to manage its repository. Wikipedia offers a distinction,

> Unlike Git, which is strictly a command-line tool, GitHub provides a Web-based graphical interface and desktop as well as mobile integration.

Incidentally, GitHub uses Jekyll to power GitHub Pages. Therefore, it is because I chose GitHub Pages as my web server, that I came to use Jekyll as my scaffold. I edit my blog locally on my computer through Terminal (the command line interface for Apple's OS X), and push changes to my website through GitHub.

I should further note that the theme of this blog was designed by [Heiswayi Nrird](http://heiswayi.github.io), who I think has captured the spirit of minimalism quite well, given that this site combines both blog and portfolio. 

### Jekyll in Terminal

Build entire site.

```shell
jekyll build
```

Build only files that have been modified.

```shell
jekyll build --incremental
```

## Git Cheat Sheet

### Flags

| Flag | Long form | Meaning |
| ---- | --------- | ------- |
| -a | --all | Automatically stage all modified files but not new files. |
| -m &lt;msg&gt; | --message=&lt;msg&gt; | Use the given <msg> as the commit message. |
| -C &lt;commit&gt; | --reuse-message=&lt;commit&gt; | Reuse the log message and authorship from &lt;commit&gt;. |

### Commits

Record changes to repository for all modified files with specified commit message.

```shell
git commit -a -m "Commit message."
```

Commit using most recent commit and message.
```shell
git commit --amend --no-edit
```


### Pushing Changes

Push stuff... idk...

```shell
git push origin master
```

### Revert commits

Still working on figuring this out. 


## LaTeX Formatting

### Setup

Add the MathJax script into the <code>&lt;head&rt;</code> block of page.

```html
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
```

### Equations

In Markdown, surround equations with double dollar signs.

$$\frac{\delta E_{x}}{\delta t} = \frac{\delta f(z-ct)}{\delta t} = f^{\prime}(z - ct)\Big(\frac{\delta(z-ct)}{\delta t}\Big) = -c*f^{\prime}(z - ct)$$

```latex
$$\frac{\delta E_{x}}{\delta t} = \frac{\delta f(z-ct)}{\delta t} = f^{\prime}(z - ct)\Big(\frac{\delta(z-ct)}{\delta t}\Big) = -c*f^{\prime}(z - ct)$$
```
