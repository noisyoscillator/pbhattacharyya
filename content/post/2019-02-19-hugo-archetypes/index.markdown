---
authors:
- alison
categories:
- hugo
- blogdown
date: "2019-02-19"
image:
  caption: '[Photo by Joanna Kosinska on Unsplash](https://unsplash.com/photos/Prfs32wh-o4)'
  focal_point: center
summary: Why you should use Hugo archetypes in your blogdown site
tags:
- blogdown
title: 'A Spoonful of Hugo: Archetypes'
---

> "Just a spoonful of Hugo helps the blog go down."
- me, only somewhat kidding

As a happy blogdown user, a common story I hear from other #rstats users is that you try to change one little thing in Hugo, and the whole site breaks. [Here be dragons](https://en.wikipedia.org/wiki/Here_be_dragons) for folks who aren't web developers. 

![](https://upload.wikimedia.org/wikipedia/commons/e/ea/Carta_Marina.jpeg)

I'm here to tell you that there are small spoonfuls of Hugo that can help you get your site _UP_ (and even better- more efficient, more streamlined, more automated), even if you are not in the least bit interested in transitioning into a career in web development 😏.



## My Project

The education team at RStudio needs a website and we have a short wishlist:

- We want something we can maintain ourselves, 
- We want to look consistent with other RStudio sites on the outside, and 
- We want to be consistent on the inside so that we can get help if/when we need it.

This led me to the current [tidyverse.org](https://www.tidyverse.org/) blogdown site. I wanted to make a copy of the site then customize for the education team, but I noticed that the [source code](https://github.com/tidyverse/tidyverse.org) for the site didn't make it easy for me to copy the *structure* of the site and edit only the *content* of the site. This is one of the real strengths of Hugo, so I embarked on a learning adventure.

<center>
<iframe src="https://giphy.com/embed/VGG8UY1nEl66Y" width="480" height="392" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/adventure-latin-flinch-VGG8UY1nEl66Y">via GIPHY</a></p>
</center>


As a result, I have been living and breathing Hugo lately. As in, my husband now recognizes [Mike Dane's voice](https://www.mikedane.com/). You may not have have met Mike yet, but he appears in all the video tutorials in the [Hugo docs](https://gohugo.io/documentation/). His screencasts have been really helpful to me, like this [one on templating](https://gohugo.io/templates/introduction/). I've also spent a lot of time actually reading the [docs](https://gohugo.io/documentation/) (which are pretty good!), reading posts and answers on the [Hugo discourse community site](https://discourse.gohugo.io/), and spelunking around inside the actual source code for two very well structured Hugo sites:

1. The actual [Hugo](https://gohugo.io/) site: https://github.com/gohugoio/hugoDocs
2. The [rOpenSci](https://ropensci.org/) site: https://github.com/ropensci/roweb2

I'll be using this post and other later posts to share some of the things I've learned about Hugo along the way. Mainly breadcrumbs to myself, but I hope these help other people too.

For reference, I'm using Hugo via the [blogdown R package](https://bookdown.org/yihui/blogdown/), and within the [RStudio IDE](https://www.rstudio.com/products/rstudio/#Desktop). These are my [blogdown](https://github.com/rstudio/blogdown) and Hugo versions:


```r
packageVersion("blogdown")
```

```
## [1] '0.21.61'
```

```r
blogdown::hugo_version()
```

```
## [1] '0.79.0'
```


## tl;dr: A Teaspoon of Archetypes

1. Add custom archetypes as `.md` files to your project root directory (do *not* touch the `archetypes` folder in your `themes/archetypes` folder). 
    - If you don't have that as an empty folder in your project root, make one, then add your archetype files to it.
    - If you are making a new blogdown site, I recommend using [these options](https://arm.rbind.io/slides/blogdown.html#start-here) to __keep your empty directories__^[These setup options are newish to the blogdown package: https://github.com/rstudio-education/arm-workshop-rsc2019/issues/8]:

    
    ```r
    library(blogdown)
    new_site(theme = "jpescador/hugo-future-imperfect", 
             sample = TRUE, 
             theme_example = TRUE, 
             empty_dirs = TRUE, # this!
             to_yaml = TRUE)
    ```

    <div class="figure">
    <img src="https://arm.rbind.io/slides/img/blogdown-workflow-wizard.png" alt="Using the RStudio Project Wizard"  />
    <p class="caption">(\#fig:proj-wizard)Using the RStudio Project Wizard</p>
    </div>



1. Use the "New Post" Addin in RStudio to create __any and all__ new content for your site (not just *posts*!). Be sure to use the handy dropdown menu to select from all the possible archetypes. Also, careful about the subdirectory here- some themes use *blog*, others use *news*, *articles*, or *posts*.

    ![](https://arm.rbind.io/slides/img/blogdown-newpost-bundle.png)<!-- -->

1. Your archetypes, while only markdown files, *can* include R code. When you use the Addin, be sure to choose `R Markdown (.Rmd)` as the format so that you can run the code.
    - Don't miss this [great blog post](http://lcolladotor.github.io/2018/03/08/blogdown-archetype-template/) by my friend and the great educator [Leo Collado-Torres](https://twitter.com/fellgernon) on archetypes.


## A Tablespoon of Archetypes


One of the easiest things you can do for yourself is customize your site's archetypes. From the [Hugo docs](https://gohugo.io/content-management/archetypes/):

> "Archetypes are templates used when creating new content."

Right away when I cloned the tidyverse site, I noticed that there were instructions for how to contribute a new article (or blog post) in the [`README.md`](https://github.com/tidyverse/tidyverse.org/blob/c0eb070017cab794029b8ed3ac518f6e1a245a2b/README.md) and in a separate [`CONTRIBUTING.md`](https://github.com/tidyverse/tidyverse.org/blob/c0eb070017cab794029b8ed3ac518f6e1a245a2b/CONTRIBUTING.md) file. Then I noticed this [open GitHub issue](https://github.com/tidyverse/tidyverse.org/issues/113) from [Mara Averick](https://twitter.com/dataandme) (the tidyverse developer advocate) titled "Fix README/CONTRIBUTING so there's one source of mechanical info?". 

I also noticed that there was no project root folder called `archetypes`, which is where you would store your custom site archetype files as `.md` files. In fact, there is no **theme** folder as you might expect either, which is where you could view the default theme archetypes. Let's look at some from other Hugo themes:

1. The default Hugo theme for blogdown, [Lithium](https://github.com/yihui/hugo-lithium), has just one archetype: [`default.md`](https://github.com/yihui/hugo-lithium/tree/master/archetypes)

    ```yaml
    ---
    title: ''
    date: ''
    ---
    ```
  
1. In contrast, the [Hugo Academic theme](https://github.com/gcushen/hugo-academic) has A LOT: https://github.com/gcushen/hugo-academic/tree/master/archetypes; here is the content of the one for new posts:

    ```toml
    +++
    title = "{{ replace .Name "-" " " | title }}"
    subtitle = ""
    
    # Add a summary to display on homepage (optional).
    summary = ""
    
    date = {{ .Date }}
    draft = false
    
    # Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
    authors = []
    
    # Tags and categories
    # For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
    tags = []
    categories = []
    
    # Projects (optional).
    #   Associate this post with one or more of your projects.
    #   Simply enter your project's folder or file name without extension.
    #   E.g. `projects = ["deep-learning"]` references 
    #   `content/project/deep-learning/index.md`.
    #   Otherwise, set `projects = []`.
    # projects = ["internal-project"]
    
    # Featured image
    # To use, add an image named `featured.jpg/png` to your page's folder. 
    [image]
      # Caption (optional)
      caption = ""
    
      # Focal point (optional)
      # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
      focal_point = ""
    +++
    ```
    
A quick note: you may have noticed differences in both the content between these two files but also the structure. The first is a [YAML file](https://learnxinyminutes.com/docs/yaml/), the second is a [TOML file](https://learnxinyminutes.com/docs/toml/). For blogdown users, you may want to use YAML. This is also why I recommend when you set up your site to use the `to_yaml = TRUE` option (in the Project Wizard from figure <a href="#fig:proj-wizard">1</a>, check the "Convert all metadata to YAML" box; otherwise, the exampleSite will contain TOML instead of YAML)^[If you end up with TOML in your content files, run this R code: `hugo_convert(to = "YAML", unsafe = TRUE)`].

If you read the original tidyverse [`CONTRIBUTING.md`](https://github.com/tidyverse/tidyverse.org/blob/c0eb070017cab794029b8ed3ac518f6e1a245a2b/CONTRIBUTING.md) file, the instructions include a fair bit of R code that I would guess means a lot of copying and pasting into new posts. For example, the R Markdown setup chunk and the code for using `usethis::use_tidy_thanks()` for package releases. I studied the contributing guidelines, and parsed three different "kinds" of articles that are commonly contributed, each with a different archetype:

1. The `default.md`- this is just for plain old markdown posts and basically sets up the YAML of the post to be the same as it is now (currently, there is no archetype dictating the content- it is pulling from a project-level [.Rprofile](https://github.com/tidyverse/tidyverse.org/blob/master/.Rprofile)).

1. A `default-rmarkdown.md` which should only be used with an R Markdown post and provides only the setup chunk at the top.

1. A `package-release.md` which also should only be used with an R Markdown post and adds the `usethis::use_tidy_thanks()` code chunk (this is pseudo-code so the default chunk option is set to `eval = FALSE`).

So I drafted a [pull request](https://github.com/tidyverse/tidyverse.org/pull/271) that adds [these three archetypes](https://github.com/tidyverse/tidyverse.org/pull/271/commits/26a07ae881e57607e25ef0add77d0f5958a9c143) to the [GitHub repository](https://github.com/tidyverse/tidyverse.org) for the [tidyverse.org](https://www.tidyverse.org/). Here is the "after" Addin view:

![](archetypes-after.png)


Here's hoping Hugo archetypes make some things about adding new content to your site easier. There is no Hugo involved, other than realizing that Hugo will look first in your `themes/<THEME-NAME>/archetypes/` folder, then in your project root `archetypes/` folder next. [DO](https://twitter.com/apreshill/status/1083791211222073344) [NOT](https://twitter.com/apreshill/status/1078494406301212672) [TOUCH](https://arm.rbind.io/slides/blogdown.html#35) any files in your `themes/` directory.^[Trust me on this one- if you ever want to update your site this will make that process way harder.]

You may want to set up archetypes for your blogdown site if you have a "signature" R setup chunk that loads your preferred `knitr` chunk options, common libraries you always load at setup like `tidyverse`, `ggplot2` themes you prefer (`theme_minimal()` FTW), etc. This may be especially helpful if you have multiple team members contributing to a single site and you want their posts to have a uniform setup. Then archetypes can be a real time- and sanity-saver. Get more ideas from Leo's [blog post](http://lcolladotor.github.io/2018/03/08/blogdown-archetype-template/) on archetypes. You *can* also make [directory based archetypes](https://gohugo.io/content-management/archetypes/#directory-based-archetypes) if you use Hugo page bundles, which is a topic of a future post.
