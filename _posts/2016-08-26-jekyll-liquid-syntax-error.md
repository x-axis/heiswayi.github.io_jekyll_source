---
layout: post
title: Liquid Syntax Errors in Jekyll 3.2.1
description: All I wanted to do was put in an image. Bug log.
---
Two days ago, I encountered the following error message when building my site:

```shell
Asset inconsitency, expected
jekyll 3.1.6 | Error: undefined method `logical_path' for nil:NilClass
```
I hadn't encountered this before, so I just ran <code>jekyll clean</code> which flushed my caches and everything in <code>/_site/</code>. Well, it fixed the error but then I got a new one:

```shell
Liquid Exception: Liquid syntax error (line 12): Unknown tag 'img' 
```

For the record, this is how I was inserting images in my Markdown:

```shell
{% raw %}{% img river-tubing.jpg %}{% endraw %}
```

Quick and easy. I fixed it with [this workaround](https://superdevresources.com/image-caption-jekyll/) (with new image captioning support). Now I would insert images like this:

```shell 
{% raw %}{% include image.html
	img="images/river-tubing.jpg"
	caption="Image from Trinity River Vision Authority." %}{% endraw %}
```

But I was REALLY SAD that the original method didn't work. Why?! So I upgrade from Jekyll 3.1 to 3.2.1 to see if it worked -- it didn't. Well, then I found out that my images weren't copying over in Jekyll because they were never being referenced. 

I saw a [similar complaint](http://stackoverflow.com/questions/17990087/why-images-folder-is-not-copied-when-generating-an-octopress-with-jekyll-assets) and tried the following solution:

```shell
{% raw %}{% asset_path river-tubing.jpg %}{% endraw %}
```

Which would give me the following error:

```shell
Liquid syntax error (line 12): Unknown tag 'asset_path'
```

So it's not an issue with Jekyll, it's an issue with my configuration. At this point I have spent enough time on it and really want to get back to my bluetooth project.

