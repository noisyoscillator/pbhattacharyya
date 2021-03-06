---
author: Alison Hill
authors:
- alison
categories:
- hugo
- blogdown
- netlify
- rmarkdown
date: "2020-12-31"
image:
  caption: '[Photo by Ben Wilkins on Unsplash](https://unsplash.com/photos/8Yxkb0SvNEM)'
  focal_point: ""
slug: new-year-new-blogdown
summary: New year, new blogdown! A guide to getting up and running with blogdown,
  the Hugo Wowchemy starter-academic theme, GitHub, and Netlify. Not brief.
tags:
- hugo
- blogdown
- netlify
- rmarkdown
title: Up & running with blogdown in 2021
---




## Welcome

Hi! Hello! Welcome. Bienvenidos.

About 3.5 years ago, I wrote my [first blog post](/post/2017-06-12-up-and-running-with-blogdown/) and published it on my first website. Since then, that single post has been viewed over 27,557 times. That may not seem like a lot to some folks, but it is to me! Even more meaningful to me, though, has been watching the launches of so many people's personal websites.

![](https://media.giphy.com/media/BU5j1oVls8rXG/giphy.gif)


However, the process of creating and maintaining a Hugo website using blogdown was not always pain-free. Sometimes we have Hugo "improvements" to thank, other times your Hugo theme is at fault, and sometimes we could blame blogdown. Regardless of where the pain came from, there was definitely room for improvement.

![](https://media.giphy.com/media/KTyJ3VPxkbDKU/giphy.gif)

Here are some great blog posts that document pretty common user experiences and frustrations:

+ [Maëlle Salmon's post: *What to know before you adopt Hugo/blogdown*](https://masalmon.eu/2020/02/29/hugo-maintenance/)

+ [Athanasia Mowinckel's post: *Changing your blogdown workflow*](https://drmowinckels.io/blog/2020-05-25-changing-you-blogdown-workflow/)

+ [Claus Wilke's post: *Writing a blogdown post for the ages*](https://clauswilke.com/blog/2020/09/08/a-blogdown-post-for-the-ages/)


All of this, combined with my own experiences teaching and using blogdown for over 3.5 years led me to...my giant blogdown wishlist. I had a lot of ideas to help beginners get started, but just as important, to improve the quality of life for existing users. You can see my mega-wishlist that Yihui Xie (the blogdown conceptor and author) asked me to share with him: https://github.com/rstudio/blogdown/issues/476

I'm very happy to report that our team has been working very hard to address these issues, and many others raised by users, to make blogdown easier to learn and use. Just in time for the new year, we have a new and improved release of the blogdown package for you to test. I know a lot of folks are itching to introduce themselves into online communities and conversations, so I thought it would be fun to take my original blogdown post, and trace the same process of building a Hugo website with the same theme (now named ["Wowchemy"](https://wowchemy.com/) instead of Hugo Academic- don't get me started).

So if you are feeling fearless and want to live on the bleeding edge, read on to give the development version of blogdown a spin along with me.

![](https://media.giphy.com/media/42zi6wvKUbXHbzwBbD/giphy.gif)

## tl;dr

If you already know what you are doing, this entire post can be condensed into just a few lines of code:


```r
remotes::install_github("rstudio/blogdown")
usethis::create_project()
blogdown::new_site(theme = "wowchemy/starter-academic")
blogdown::serve_site()
blogdown::new_post(title = "Hi Hugo", 
                     ext = '.Rmarkdown', 
                     subdir = "post")
usethis::use_git()
usethis::use_github() # requires a GitHub PAT
```

The above sequence is a slightly more advanced workflow than the steps I follow below, but is fairly magical- attempt at your own risk! For everyone else, read on...

## Pre-requisites

Getting any website up and running with all the moving parts (RStudio, GitHub, Hugo, Netlify) can take a few tries. In this post, I'm passing along what works for me, and the workflow that I use when I teach Hugo website development. Everyone's mileage may vary, though, depending on your operating system and your approach. 

For this blog post, I'm assuming you have basic familiarity with:

+ R, 
+ the RStudio IDE, and 
+ GitHub. 

If that is not you, you will need to work through [Happy Git with R](http://happygitwithr.com) by Jenny Bryan et al. first, then come back here when you are ready. 

Since the development version of blogdown is currently only available on GitHub, you may need to setup a [GitHub Personal Access Token](https://happygitwithr.com/github-pat.html) to install it. 

In my original 2017 post, I mentioned that at that time, I was a new mom, and just in the process of writing all that up, I filled up my tea mug twice with ice cold water, and filled my water bottle with scalding hot water. This time around isn't too different! Fast forward to 2020: there is a global pandemic, I've been under stay-at-home orders with a child under 5 years of age at home for months. So buckle up :cowboy:

![](https://media.giphy.com/media/Q9vJgdNPoyKSA6APDo/giphy.gif)

{{% alert note %}}
I've included code chunks below using the [rstudioapi](https://rstudio.github.io/rstudioapi/) package to help you navigate to the right file at the right time. Hugo sites have a dizzying and heavily nested directory structure! You'll need to run `install.packages("rstudioapi")` to use those code chunks, but you can also navigate on your own to the file you need too.
{{% /alert %}}

## Step 0: Set your intentions

![](00-blogdown-2021.gif)

During workshops, I try to set aside some time at the start for folks to set their website intentions. This might feel a bit like navel-gazing, but trust me here. I know you just want to jump in and get started! 

Hear me out though, and don't skim or skip this step. The process of actually building and deploying a personal site can be complicated, and it is easy to get lost in the weeds. 

![](https://media.giphy.com/media/l3vRbcJ60KOxd9bVu/giphy.gif)

It is very easy to run out of steam when it is time to do the most fun and important piece: dreaming about the kind of site you want to make!

{{% alert todo %}}
Do this right now! Take 10 minutes to set your website intentions---grab a pen and notepad and a cup of 🍵 and read on...
{{% /alert %}}

### 1. Content {#todo-content}

Hugo is made for blogs. But, in addition to a blog, the starter-academic theme provides a unique system of widgets. You can have one or many widgets on pages in your site. I like to think of widgets like [Mr. Potato Head](https://en.wikipedia.org/wiki/Mr._Potato_Head) where:

+ Each page is a potato head, and 
+ Each widget is a piece you could place on the potato head. 

![](https://media.giphy.com/media/tjGVkrPMjngt2/giphy.gif)

Take the homepage for example, seen on the [Academic demo site](https://academic-demo.netlify.app/). Each band or section you see is a widget. Widgets can be stand-alone pages, or can be combined on a single page. 

Examples:

+ Multiple widget page: my [resume](/resume/) and [about](/about/) pages
+ Single widget page: my [projects](/projects/)

{{% alert todo %}}
Look at the [Academic demo site](https://academic-demo.netlify.app/) and write down some widgets you see that you like, and the ones you definitely don't.
{{% /alert %}}

### 2. Menu {#todo-menu}

Now that you have a sense of the content you want, how do you want a visitor to be able to explore your content? I typically recommend limiting the top navbar to 5 links max (excluding the search icon). 

Use some of my favorite personal sites (that do not use our theme) as inspiration too:

+ https://www.jason.af/
+ https://www.nistara.net
+ https://third-bit.com/
+ https://maggieappleton.com/
+ https://www.drcathicks.com/
+ https://amber.rbind.io/
+ https://dscott.netlify.app/
+ https://drmowinckels.io/

Think about how the menu "prewires" you to know what to expect as you dig deeper into their site. How do you want people to get to know you online?

{{% alert todo %}}
Write down up to 5 items to appear in your upper navbar.
{{% /alert %}}

### 3. Homepage {#todo-home}

This is the first page a visitor lands on when they find your site. Think of it like a welcome mat. Do you like a single page site where you scroll and see everything on one page? Or do you prefer a short and sweet homepage? Do you want a photo and a bio to be the first thing visitors see? What else?
    
Here are some examples of personal websites built with the Hugo Academic theme to inspire you:

+ https://malco.io/
+ https://isabella-b.com/
+ https://www.connorrothschild.com/
+ https://silvia.rbind.io/
+ https://maya.rbind.io/
+ https://www.allisonhorst.com/
+ https://juliasilge.com/
+ https://desiree.rbind.io/

{{% alert todo %}}
Write down the widgets you want to see on your homepage. It can be one, or many.
{{% /alert %}}

OK, keep these notes handy! We are ready to *make something.*

![](https://media.giphy.com/media/mXqtfNsJlKtAoyLHd4/giphy.gif)

## Step 1: Create repo

![](01-blogdown-2021.png)


1. Go online to your [GitHub](https://github.com) account, and create a new repository (check to initialize with a `README` but don't add `.gitignore`- this will be taken care of later). For naming your repo, consider your future deployment plan:

      ![Screenshot above: Creating a new repository in GitHub](github-new-repo.png)

      + [**Netlify**](https://www.netlify.com). I recommend using Netlify to *both* build and host your site. In this case, you can name the repository anything you want! 
      
      + [**GitHub Pages**](https://pages.github.com). I recommend Netlify over GitHub Pages for blogdown/Hugo sites. But, if you want to host your site with GitHub Pages, you should name your repository `yourgithubusername.github.io` (so mine would have been `apreshill.github.io`). This post won't be able to help you with publishing.

{{% alert note %}}
You can see some of the repo names used by members of the `rbind` organization [here](https://github.com/rbind/repositories). 
{{% /alert %}}


2. Go to the main page of your new repository, and under the repository name, click the green **Clone or download** button.

3. Choose either SSH or HTTPS (if you don't know which, choose HTTPS). Choose by clicking on the clipboard icon to copy the remote URL for your new repository. You'll paste this text into RStudio in the next section.
    
## Step 2: Create project

![](02-blogdown-2021.png)

We just created the remote repository on GitHub. To make a local copy on our computer that we can actually work in, we'll clone that repository into a new RStudio project. This will allow us to sync between the two locations: your remote (the one you see on github.com) and your local desktop.

Open up RStudio to create a new project where your website's files will live.
    
1. Click `File > New Project > Version Control > Git`.

1. Paste the copied URL from the previous step.

1. Be intentional about where you tell RStudio to create this new Project on your workstation.

1. Click **Create Project**.

    
## Step 3: Create site

![](03-blogdown-2021.png)

1. The latest version of blogdown will not be available on CRAN until January 2021, but you can install the development version from GitHub with:

    ```
    > if (!requireNamespace("remotes")) install.packages("remotes")
    > remotes::install_github("rstudio/blogdown")
    Using github PAT from envvar GITHUB_PAT
    Downloading GitHub repo rstudio/blogdown@master
    ```

1. Let's use our first blogdown function to create a website with the Hugo Wowchemy "starter-academic" project:

    ```
    > library(blogdown)
    > new_site(theme = "wowchemy/starter-academic")
    ```

1. You should now see something like this. Take a moment to read through these messages - importantly, it tells you how to start and stop the server so you can preview your site. Importantly, when you come back to your project, note that you can use `blogdown::serve_site()` or the "Serve Site" addin to preview it locally. 

    ![](new_hugo_start.png)

     Let's select `y` to let blogdown start a server for us.
    
    Exciting, isn't it? Now, don't trap your site in the RStudio Viewer pane. Let it out! Click to "Show in new window" (to the right of the :broom: icon) to preview it in a normal browser window. When you do that, you'll be re-directed to the site's main homepage. Let's find our way back to the R Markdown post. Click on `Posts > Hello R Markdown` to read it:
    
    ![](sample_post.png)

    This is what blogdown gives you- everything else in the site is given to you by Hugo and your Wowchemy Hugo theme. But this post, and your ability to see output and plots rendered with <i class="fab fa-r-project"></i> is what blogdown adds!

## Step 4: Create content

![](04-blogdown-2021.png)

Let's use more R Markdown :tada: 

Blogdown allows you to create new two kinds of R Markdown posts that are knittable:

+ `.Rmd` 🧶 to `.html` or 

+ `.Rmarkdown` 🧶 to `.markdown`

Once knitted, both are then previewable in your Hugo site.

{{% alert note %}}
I used to agonize over which file extension to use. But now I am squarely in `.Rmarkdown` camp with [Maëlle](https://masalmon.eu/2020/02/29/hugo-maintenance/)- I like knitting to `.markdown` and wish this was easier in blogdown; see: https://github.com/rstudio/blogdown/issues/530 
{{% /alert %}}

Use the console to author a new `.Rmarkdown` post; I'll name my post "Hi Hugo":

```
> blogdown::new_post(title = "Hi Hugo", 
                     ext = '.Rmarkdown', 
                     subdir = "post")
```

This takes the path to where you want your post to live, relative to the `content/` folder (so that piece of the path is assumed, rightly so!). In the Academic theme, the example site organizes blog posts into the `content/post/` folder, but the name of this folder varies across Hugo themes. 

{{% alert note %}}
A rule that is true 90% of the time: folders in `content/` are singular, not plural--- :heavy_check_mark: `post`; :x: `posts`
{{% /alert %}}

You can add an option to your `.Rprofile` to save these settings so you don't have to remember them:


```r
# if exists, opens; if not, creates new
blogdown::config_Rprofile() 
```

Then add the blogdown options to that file, save, and **RESTART YOUR R SESSION** for changes to take effect:

```
options(
  # to automatically serve the site on RStudio startup, set this option to TRUE
  blogdown.serve_site.startup = FALSE,
  # to disable knitting Rmd files on save, set this option to FALSE
  blogdown.knit.on_save = FALSE     <- change
  blogdown.author = "Alison Hill",  <- add
  blogdown.ext = ".Rmarkdown",      <- add
  blogdown.subdir = "post"          <- add
)
```

{{% alert warning %}}
Always restart your R session after editing your `.Rprofile` for changes to take effect. Don't forget to run `serve_site()` after a restart.
{{% /alert %}}

If you look in your **Files** pane, you can see that this creates a folder with the date and the ["slug"](https://en.wikipedia.org/wiki/Clean_URL#Slug) name of my post (`"hi-hugo"`). The actual R Markdown file is named `index.Rmarkdown`. 

![](new_post.png)

This is a Hugo [page bundle](/post/2019-02-21-hugo-page-bundles/). Each post gets its own bundle, or folder. Inside the post bundle is where all your static images, static data files like `.csv` files should go. 

```
content/
├── posts
│   ├── 2021-01-01-hi-hugo
│   │   ├── bakers.csv
│   │   ├── image1.jpg
│   │   ├── image2.png
│   │   └── index.Rmarkdown
```

In the post itself, use the relative file path like:

```
![my-first-image](image1.jpg)
```

Let's look at the `index.Rmarkdown`. We'll knit this `.Rmarkdown` to a `.markdown` file. You may 🧶 knit 🧶 freely now in blogdown! 

![](https://media.giphy.com/media/iBjylURwS9N9FCl8Dl/giphy.gif)


To knit an `.Rmarkdown` post, you can either:

1. Use the Knit button to knit to the correct output format, or

1. Use the keyboard shortcut `Cmd+Shift+K` (Mac) or `Ctrl+Shift+K` (Windows/Linux).

After knitting, you should now see:

```
content/
├── posts
│   ├── hi-hugo
│   │   ├── bakers.csv
│   │   ├── image1.jpg
│   │   ├── image2.png
│   │   ├── index.Rmarkdown
│   │   └── index.markdown   <- 🆕
```

Go ahead and add an R code chunk like:

````
```{r}
summary(Orange)
```
````

After you edit your `.Rmarkdown` post, knit. Note that knitting automatically saves the file for you. You also can just save the file without knitting- this is good for when your code still needs work and won't run as is.

{{% alert note %}}
The most important thing here is to realize that the act of knitting creates an `index.markdown` file in the same post bundle as `index.Rmarkdown`. Because Hugo doesn't know R or R Markdown, The `index.markdown` version is what then feeds into the Hugo static site generator.
{{% /alert %}}

Try it again! Add another R code chunk like:

````
```{r echo=FALSE}
library(ggplot2)
oplot <- ggplot(Orange, aes(x = age, 
                   y = circumference, 
                   colour = Tree)) +
  geom_point() +
  geom_line() +
  guides(colour = FALSE) +
  theme_bw()
oplot
```
````

Knit, and you should see something like:

![](post-plot.png)


{{% alert warning %}}
Many R Markdown output options for HTML documents are not going to be possible here, like tabbed sections, floating table of contents, the `code_download` button, etc. Also, HTML widgets are a little dicey currently.
{{% /alert %}}

This is a single page. It is made with R Markdown, and happens to be a blog post, although you can use R Markdown to create content for any other content section too. 

If you want a featured image to accompany your post and show up on your listing page (the clickable list of all your posts), you'll want to add an image with the word `featured` in the filename:

```
content/
├── posts
│   ├── hi-hugo
│   │   ├── bakers.csv
│   │   ├── image1.jpg
│   │   ├── image2.png
│   │   ├── index.Rmarkdown
│   │   ├── index.markdown   
│   │   └── featured-bakers.jpg   <- ➕
```

### Workflow

My workflow in RStudio at this point (again, just viewing locally because we haven't deployed yet) works best like this:

1. Open the RStudio project for the site.

1. Start the Hugo server using `blogdown::serve_site()` (only once due to the magic of *LiveReload*).

1. View site in the RStudio viewer pane, and open in a new browser window while I work.

1. Select existing files to edit using the file pane in RStudio.

1. After making changes, save if a plain `.md` file, or if working with an `.Rmd` or an `.Rmarkdown` document, `knit` to preview! You can now use the Knit button to knit to the correct output format. You can also use the keyboard shortcut `Cmd+Shift+K` (Mac) or `Ctrl+Shift+K` (Windows/Linux).

1. The console will detect the change (it will print `Change detected, rebuilding site.`), the viewer pane will update, and (in a few seconds) your local view in your browser will also refresh. Try to avoid hitting the refresh button in your browser.

1. When happy with changes, add/commit/push changes to GitHub.

Having `blogdown::serve_site` running locally with *LiveReload* is especially useful as you can immediately see if you have totally screwed up. For example, in editing my `about.md` file, this error popped up in my console after making a change and I was able to fix the error right away:

```
Started building sites ...
ERROR 2017/06/08 16:22:34 failed to parse page metadata for home/about.md: (18, 6): missing comma
Error: Error building site: Errors reading pages: Error: failed to parse page metadata for home/about.md: (18, 6): missing comma for about.md
```

### Using GitHub

Let's go ahead and push our changes to GitHub. First, let's make a `.gitignore` file:


```r
file.edit(".gitignore")
```

Add this content:

```
.Rproj.user
.Rhistory
.RData
.Ruserdata
.DS_Store
Thumbs.db
```

### Check yourself before you wreck yourself

Let's use blogdown to check this file before we do our first commit:

```r
blogdown::check_gitignore()
```

You should see something like:
```
> check_gitignore()
― Checking .gitignore
| Checking for items to remove...
○ Nothing to see here - found no items to remove.
| Checking for items you can safely ignore...
○ Found! You have safely ignored: .DS_Store, Thumbs.db
| Checking for items to ignore if you build the site on Netlify...
● [TODO] When Netlify builds your site, you can safely add to .gitignore: public, resources
― Check complete: .gitignore
```

You have a `[TODO]` item- go ahead and add `public` and `resources` on their own lines in your `.gitignore` file. We'll be configuring Netlify to build our site shortly, so go right ahead while the file is open. 

While we are at it, let's check out our content too:


```r
blogdown::check_content()
```

You may notice a few pieces of content are flagged as `draft`. This is good to know! Read up on drafts in Hugo [here](https://bookdown.org/yihui/blogdown/content.html#yaml-metadata).

Our checks are pretty clean, so you can freely add/commit your project files to GitHub. You now should have the basic mechanics of your site working.

## Step 5: Publish site

![](05-blogdown-2021.png)

Thus far, we've only been previewing our site locally, then pushing the source files (but not the built site) to GitHub. This workflow works, but I assume you want to ride this bike. Let's skip the training wheels &mdash; we are going one step more advanced by using GitHub with Netlify now.

{{% alert note %}}
Note that you could use `blogdown::build_site()`, then publish the `public/` folder using Netlify [drag & drop](https://app.netlify.com/drop). Watch this [webinar](../talk/2020-sharing-short-notice/) called "Sharing on Short Notice" to learn more - but this is a less advanced workflow.
{{% /alert %}}

To get started using Netlify for real (which has a free plan that should largely cover recreational blogging use!):

1. Go online to [Netlify](https://www.netlify.com). 

1. Click on the **Sign Up** button and sign up using your existing GitHub account (no need to create another account).

1. Log in, and select: `New site from Git > Continuous Deployment: GitHub`.

1. From there, Netlify will allow you to select from your existing GitHub repositories. You'll pick the repo you've been working from with `blogdown`. Leave all settings as they are and select **Deploy Site**.

You should see something like this:

![](new_netlify.png)

When it is done, you can click on the link to your new site! And the most magical thing of all, every time you push any changes to your site to GitHub, Netlify will detect the push, re-build, then update your published site. It's a good thing. It's called continuous deployment, and it is the main reason to use Netlify for a blogdown site.

With a new site, Netlify will deploy your site and assign you a random subdomain name of the form `random-word-12345.netlify.app`. Mine was particularly unfortunate, with the random word `garbage-collector-janice`. You should know that you can change this; I changed mine to `apreshill.netlify.app`. Do this by navigating to your site on Netlify, then click on **Settings**. Under **Site information**, click on the *Change site name* button.

![](netlify-site-name.png)

Whether you change your Netlify site name or use the random one, go back to your configuration file and cchange the baseurl there to match where Netlify is publishing your site:


```r
rstudioapi::navigateToFile("config.yaml", line = 3)
```

You actually have most of the necessary wiring laid out for you already in your repo, which is why this worked. Our site has a `netlify.toml` file, which sets us the necessary settings for letting Netlify build our site for us and then publish it. You can read more about this file [here](/post/2019-02-19-hugo-netlify-toml/), and check it out using:


```r
# if exists, opens; if not, creates new
blogdown::config_netlify()
```


Now, back in your local blogdown project, let's check this file with blogdown:

```
> blogdown::check_netlify()
― Checking netlify.toml...
○ Found HUGO_VERSION = 0.79.1 in [build] context of netlify.toml.
| Checking that Netlify & local Hugo versions match...
| Mismatch found:
  blogdown is using Hugo version (0.79.0) to build site locally.
  Netlify is using Hugo version (0.79.1) to build site.
● [TODO] Option 1: Change HUGO_VERSION = "0.79.0" in netlify.toml to match local version.
● [TODO] Option 2: Use blogdown::install_hugo("0.79.1") to match Netlify version, and set options(blogdown.hugo.version = "0.79.1") in .Rprofile to pin this Hugo version.
| Checking that Netlify & local Hugo publish directories match...
○ Good to go - blogdown and Netlify are using the same publish directory: public
― Check complete: netlify.toml
```

I recommend going with `Option 1` here, so follow that `[TODO]` and then run the function again to get a clean check.

When you are ready to deploy, commit your changes and push to GitHub! Watch as your site rebuilds :tada:

{{% alert note %}}
To get an `*.rbind.io` URL, follow [these instructions](/post/2017-06-12-up-and-running-with-blogdown/#rbindio-domain-names).

Anytime you change your subdomain name, you need to update the `baseurl` in your `config.toml` file (so I changed mine to baseurl = "https://apreshill.netlify.com/").
{{% /alert %}}


## Step 6: Sculpt site

![](06-blogdown-2021.png)

Now, we'll leave blogdown and R Markdown behind. We'll just be using Hugo and Wowchemy (I think it is said like alchemy? Why??) to build your personal website.

Let's start by running another blogdown check to `check_hugo()`:

```
> blogdown::check_hugo()
― Checking Hugo
| Checking Hugo version...
○ Found 4 versions of Hugo. You are using Hugo 0.79.0.
| Checking .Rprofile for Hugo version used by blogdown...
○ blogdown is using Hugo 0.79.0 to build site locally.
● [TODO] Also run blogdown::check_netlify() to check for possible problems with Hugo and Netlify.
― Check complete: Hugo
```

All set! We've already checked out our Netlify set-up :heavy_check_mark: If you wish to clean up your local Hugo installations, check out:


```r
blogdown::remove_hugo()
```

### Configure your site

Let's start with the last thing you typically do to your home- decorate.

Open up the file `config/_default/params.toml`. Play with any of these configurations, but especially fonts/themes. 



```r
rstudioapi::navigateToFile("config/_default/params.toml")
```

{{% alert note %}}
If you want deeper customization of the styling, you can create a new CSS file `assets/scss/custom.scss` and use it to override any existing styles. You can see mine [here](https://github.com/rbind/apreshill/blob/master/assets/scss/custom.scss); heavily borrowing from my former intern [Desirée De Leon](https://desiree.rbind.io/)!
{{% /alert %}}

While you are at it, edit the other configuration files:

* You can also view [my `config.toml` file](https://github.com/rbind/apreshill/blob/master/config.toml)

Remember our [menu intentions](#todo-menu)? Go ahead and edit those too:


```r
rstudioapi::navigateToFile("config/_default/menus.toml")
```



Let's run a blogdown check on the configuration file before we leave:

```
> blogdown::check_config()
― Checking config.yaml
| Checking "baseURL" setting for Hugo...
○ Found baseURL = "https://silly-dubinsky-de5482.netlify.app"; nothing to do here!
| Checking "ignoreFiles" setting for Hugo...
● [TODO] Add these items to the "ignoreFiles" setting: "\\.Rmd$", "\\.Rmarkdown$", "\\.knit\\.md$", "\\.utf8\\.md$"
| Checking setting for Hugo's Markdown renderer...
○ All set! Found the "unsafe" setting for goldmark.
― Check complete: config.yaml
```

Looks like we have a few `[TODO]` items to add to our `config.yaml` file:


```r
rstudioapi::navigateToFile("config.yaml", line = 15)
```



### Goodbye Nelson B.

Let's say goodbye to [Nelson Bighetti](https://themes.gohugo.io/theme/academic/#about). Everything in this single markdown file populates what is called the `about` widget; a customized one looks like this:

![](about.png)


Find and open the file `content/authors/admin/_index.md`:


```r
rstudioapi::navigateToFile("content/authors/admin/_index.md")
```

Edit the YAML metadata to change:

+ The [icons](https://wowchemy.com/docs/page-builder/#icons) and where they link to

+ Your current role and organization

+ Your interests

+ Your education

The text under the YAML is your bio; you can use markdown here. Add an `avatar.jpg` file too (it *must* be named this) to the same folder.


### Prune widgets

Remember how we started with thinking about your [content](#todo-content)? We are ready to prune out some of our unwanted widgets.

Recall that on the [Academic demo site](https://academic-demo.netlify.app/), the entire home page is filled with widgets! The default example site is the exact same as the demo. It sets almost every available widget to **active** to show you the range of what you could do. 

Deactivating the widgets you don't need and only activating the ones you want will help you avoid having your home page feel like the 💀 "scroll of death," as my friend [Jackie Wirz](https://twitter.com/jackiewirz) called it. 

Remember my [Mr. Potato Head](https://en.wikipedia.org/wiki/Mr._Potato_Head) analogy? The home page is your most prominent potato, and the widgets are all the pieces you could use. 

![](https://media.giphy.com/media/305jKnp2ErJK0/giphy.gif)

Each widget you see is a `*.md` file in the `content/home/` folder. The metadata at the top helps you configure each widget; namely whether it is `active` (true or false) and the widgets `weight` (ordering, actual numbers doesn't matter- only relative to the other weights).

For example, to turn off the hero widget, use this code in your console and set `active = false`:


```r
rstudioapi::navigateToFile("content/home/hero.md", line = 5, column = 10)
```

Take about 10 minutes about try out turning widgets off and on, and changing their order to see what you like! 

{{% alert note %}}
You can also delete a widget file. You can always recover `*.md` widget files by going into your `themes/hugo-academic/exampleSite/content/home/` folder.
{{% /alert %}}

For my own site, I use 4 main home page widgets:

1. [*about*](/#about) (photo / icons / bio / interests / education)
1. [*slider*](/#slider) (used to showcase some feedback from my workshops)
1. [*posts*](/#posts) (set to show only the most recent)
1. [*talks*](/#talks) (set to show only the most recent)


### Transplant widgets

If you opted for a more streamlined home page with fewer widgets, you may experience *widget pruning regret*. Many are very useful, and you may wish to use widgets on *other* pages that are not the home page. In this theme, this is possible! Even if you turn off a widget on the home page, you can create what is called a widget page and add or even combine widgets there. I make heavy use of widget pages in my own site. Here are the steps (following the [docs](https://sourcethemes.com/academic/docs/managing-content/#create-a-widget-page)):

1. Create a new folder in `content/`; let's call it `resume`

2. Inside `content/resume/`, add a file named `index.md`

3. Populate `content/resume/index.md` with a YAML, like this:

    ```yaml
    ---
    summary: More about my work experience
    title: "Resume"
    type: widget_page
    ---
    ```
    
{{% alert note %}}
The very critical line here is the `type: widget_page`---this sets you up to now copy over widgets from `content/home/` in this new folder. 
{{% /alert %}}

4. Copy the widget `*.md` files you'd like to use into this `content/resume/` folder. Edit their metadata (weights, other info), and be sure to set `active = true`. For my own resume, I copied the *experience* and *accomplishments* widgets over.

5. If you want to access this new widget page from your top navbar, open up your `config/_default/menus.toml` and add it there, like:

    ```toml
    [[main]]
      name = "Resume"
      url = "/resume"
      weight = 50
    ```
    
{{% alert note %}}
You can link to any specific widget by taking your baseurl and appending `/#{name-of-widget}`, so `/#slider` links to [*my homepage slider*](/#slider). And `/resume/#accomplishments` links to [*my honors & awards*](/resume/#accomplishments)
{{% /alert %}}

Let's run one final check, which wraps all 5 checking functions we've used so far into a single final checklist:

```
> blogdown::check_site()
```

This is immensely comforting to me; read more about these new checking functions [here](/post/2020-12-27-blogdown-checks/).

![](https://media.giphy.com/media/j1zW1Ng86MV78tRLOo/giphy.gif)

## We made it!

At this point, you should be up and running with `blogdown`, GitHub, and Netlify. You now have the scaffold up and ready for your ideas, your style, and your voice. If you made it this far, please share your site- I'd love to see it!

![](https://media.giphy.com/media/1xNDlJsL1ntZZqm7pn/giphy.gif)
