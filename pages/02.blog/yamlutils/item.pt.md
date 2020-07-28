---
title: 'YAMLUtils: automatizar tarefas aborrecidas com Python'
metadata:
    description: Neste artigo vou mostrar como usei Python para automatizar parte da gestão do meu blogue.
---

Se há uma coisa de que gosto em programar em Python é que posso usá-lo para automatizar tarefas aborrecidas. Hoje usei-o para gerir o meu blogue!

===

![a close-up of three gears turning together](gears.jpg "Photo by Bill Oxford on Unsplash")

Vou começar por descrever o problema que tinha e depois mostro como é que Python me ajudou.
Let me start by describing what I needed to do and then I will go over how Python helped me do it.

### The problem

The fact that I am using [Grav] to manage the contents of my website and the fact that I have my website both in Portuguese and in English means I end up having two text files per page. For example, if you follow [this GitHub link][yamlutils-post] you can see the subfolder that holds the content for this particular blog post. In there you can find three main files, which are

 - `item.en.md`
 - `item.pt.md`
 - `frontmatter.yaml`

The `item` files contain the blog post itself, and the extension `.en.md` or `.pt.md` identifies the language in which they are written. To help customize my blog I can set "headers" in my posts using a special syntax called [YAML], which I use to set the post tags, the title of the post, the slug (the URL suffix, `yamlutils` for this blog post), the date in which this was published, etc.

For most of it, these things do not depend on the language the user is viewing the page on, for example I keep the slug the same for the English and Portuguese versions, cf.

 - [https://mathspp.com/en/blog/yamlutils](https://mathspp.com/en/blog/yamlutils)
 - [https://mathspp.com/pt/blog/yamlutils](https://mathspp.com/pt/blog/yamlutils)

Those headers that are the same, regardless of the language, are kept in the `frontmatter.yaml` file, which looks something like this:

<script src="https://gist.github.com/RojerGS/0ff988fb2ac54a81dc18349cc9c619f9.js"></script>



On the other hand, there are other things that _do_ depend on the language. For example, the title of the page that is displayed in the beginning of the post and in the browser tab. Those are specified in the beginning of the `item` files in between two sets of `---`, which makes GitHub render them as such:

<script src="https://gist.github.com/RojerGS/1f8f2727e6358ad33bec5700be4220ed.js"></script>



You can clearly see that while the structure of the boxes is the same, their contents are in different languages.

The problem is that for a long time I didn't use the `frontmatter.yaml` file to store the headers that were identical, meaning I have plenty of pages and blog posts that have duplicated headers in the `.pt.md` and `.en.md` files. I could sort this out by hand... but that would be really boring!


### Python to the rescue

Being a scripting language, Python excels at this type of tasks. I realized I could easily write a Python script that would traverse my blog directory, looking for pairs of `.pt.md` and `.en.md` pages, finding the headers those pages have in common, and then updating the corresponding `frontmatter.yaml` (or creating a new one if needed).

That is how my little [YAMLUtils] project was born. The [`yamlutils.py`][yamlutils.py] script takes a folder path as a command line argument (and optionally a `-r` flag to traverse the directories recursively) and then does what I just described, merging all the YAML headers it can. I used it on my blog with `python yamlutils.py pages/ -r` and you can see what it did [in this commit](https://github.com/RojerGS/mathspp/commit/7ba80b086d6987ed819c872432ef1eafc1f1b023). Imagine having to do all that by hand!


### Was it worth?

Yes.

It took me around two hours to put the script together and to test it plus ten minutes to fix a bug that I only discovered when I later applied it to the blog (cf. [this][bug-1] and [this][bug-2] buggy usages). Doing all this by hand would easily have taken me over two hours. Plus, now I have a cool new script that I can extend later (and probably will) to do some more YAML management and I programmed a bit (which is always fun!) instead of copying and pasting around YAML headers.

Let me know in the comments below how Python has helped you automate any of your tasks!

[Grav]: https://getgrav.org/
[YAML]: https://en.wikipedia.org/wiki/YAML
[xkcd]: https://xkcd.com
[yamlutils]: https://github.com/RojerGS/projects/tree/master/yamlutils
[yamlutils-post]: https://github.com/RojerGS/mathspp/tree/master/pages/02.blog/yamlutils
[yamlutils.py]: https://github.com/RojerGS/projects/tree/master/yamlutils/yamlutils.py
[bug-1]: https://github.com/RojerGS/mathspp/commit/6ac01f412bdd099eb673201689d89ea77d0370d0
[bug-2]: https://github.com/RojerGS/mathspp/commit/e97dbad13ffc6009d1160b78a83cab467b42f1ca