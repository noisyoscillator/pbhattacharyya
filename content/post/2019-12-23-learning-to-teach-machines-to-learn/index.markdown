---
author: Alison Hill
authors: []
categories: []
date: "2019-12-23"
disable_jquery: false
featured: false
image:
  caption: Image by [Daniel Cheung](https://unsplash.com/photos/sCdm5DiJb8w)
  focal_point: ""
  preview_only: false
lastmod: "2019-12-23T08:51:41-08:00"
projects: []
subtitle: ""
summary: ""
tags: []
title: Learning to Teach Machines to Learn
---

I'm excited to be teaching a new workshop at the upcoming [rstudio::conf](https://rstudio.com/conference/) in January called *"Introduction to Machine Learning with the Tidyverse"*, with my colleague Garrett Grolemund. Our workshop just sold out over the weekend! 🎉

It is always hard to develop an entirely new workshop, especially if you are doing it at the same time as learning how to use a new API. It is even harder when that API is under active development like the [**tidymodels** ecosystem](https://github.com/tidymodels)! I've been so lucky to be able to work with the tidymodels team at RStudio, [Max Kuhn](https://twitter.com/topepos) and [Davis Vaughan](https://blog.davisvaughan.com/), to help shape how we tell the tidymodels story to ML beginners. But my favorite part of developing a new workshop like this has been studying how *others* teach machine learning. Spoiler alert: there are a lot of materials intended for learners that make things seem harder than they actually are! Below, I'm sharing my bookmarked resources, organized roughly in the order I think they are most helpful for beginners.

1. **[Machine Learning for Everyone.](https://vas3k.com/blog/machine_learning/) In simple words. With real-world examples. Yes, again.** In my experience, the biggest hurdle to getting started is sifting through both the hype and the math. This is a readable illustrated introduction to key concepts that will help you start building your own mental model of this space. For example, *"the only goal of machine learning is to predict results based on incoming data. That's it."* There you go! Start here. 
    
    <a href="https://vas3k.com/blog/machine_learning/" target="_blank"><img src="https://i.vas3k.ru/7w1.jpg" width="80%" /></a>


1. [A Visual Introduction to Machine Learning by r2d3](http://www.r2d3.us/visual-intro-to-machine-learning-part-1/). This is a wonderful two-part series (that I wish would be extended!):

    + [Part I: A Decision Tree](http://www.r2d3.us/visual-intro-to-machine-learning-part-1/)
    + [Part II: Model Tuning and the Bias-Variance Tradeoff](http://www.r2d3.us/visual-intro-to-machine-learning-part-2/) <br><br>

1. [Supervised Machine Learning course by Julia Silge](https://supervised-ml-course.netlify.com/) Taught with R and the `caret` package (the precursor to the in-development **tidymodels** ecosystem), this is a great next step in your machine learning journey as you'll start *doing ML* right away in your browser using an innovative course delivery platform. You'll also get to play with data that is *not* `iris`, `titanic`, or `AmesHousing`. This will be sweet relief because you'll find the rest of my recommended resources all basically build models to predict home prices in Ames, Iowa.

    <a href="https://supervised-ml-course.netlify.com/" target="_blank"><img src="https://raw.githubusercontent.com/juliasilge/supervised-ML-case-studies-course/master/static/social.png" width="50%" /></a>
  

1. [Hands-on Machine Learning with R](https://bradleyboehmke.github.io/HOML/) by Bradley Boehmke & Brandon Greenwell. Another great way to learn concepts plus code, although another one that focuses on the `caret` package (pre-tidymodels). Each chapter maps onto a new learning algorithm, and provides a code-through with real data from building to tuning. The authors also offer practical advice for each algorithm, and the "final thoughts" sections at the end of each chapter will help you tie it all together.

    <a href="https://bradleyboehmke.github.io/HOML/" target="_blank"><img src="https://bradleyboehmke.github.io/HOML/images/homl-cover.jpg" width="40%" /></a>
    
    Don't skip the "Fundamentals" section, even if you feel like you've got that down by now. The second chapter on the [modeling process](https://bradleyboehmke.github.io/HOML/process.html) is especially good.
    
    <a href="https://bradleyboehmke.github.io/HOML/process.html" target="_blank"><img src="https://bradleyboehmke.github.io/HOML/images/modeling_process.png" width="80%" /></a>
    


1. [Interpretable Machine Learning: A Guide for Making Black Box Models Explainable](https://christophm.github.io/interpretable-ml-book/) by [Christoph Molnar](https://christophm.github.io/). If you only have time to read a single chapter, skip ahead to [Chapter 4: Interpretable Models](https://christophm.github.io/interpretable-ml-book/simple.html). I also appreciated the introduction section on [terminology](https://christophm.github.io/interpretable-ml-book/terminology.html). But the whole book is excellent and well-written.

    <a href="https://christophm.github.io/interpretable-ml-book/" target="_blank"><img src="https://christophm.github.io/interpretable-ml-book/images/title_page.jpg" width="40%" /></a>


1. **Model evaluation, model selection, and algorithm selection in machine learning- a 4-part series by [Sebastian Raschka](https://sebastianraschka.com/)**. I found this to be a great evidence-based, thorough overview of the *methods* for machine learning. I especially liked how he walks you step-by-step from the simplest methods like the holdout method up to nested cross-validation:

    + [Part I: The Basics](https://sebastianraschka.com/blog/2016/model-evaluation-selection-part1.html)
    + [Part II: Bootstrapping & uncertainties](https://sebastianraschka.com/blog/2016/model-evaluation-selection-part2.html)
    + [Part III: Cross-validation and hyperparameter tuning](https://sebastianraschka.com/blog/2016/model-evaluation-selection-part3.html)
    + [Part IV: Comparing the performance of machine learning models and algorithms using statistical tests and nested cross-validation](https://sebastianraschka.com/blog/2018/model-evaluation-selection-part4.html)
    
    <img src="https://sebastianraschka.com/images/blog/2016/model-evaluation-selection-part1/iris-dist.png" width="50%" />
    
1. At this point, if you can read through the above resources and you are no longer feeling awash in new terminology, I think your vocabulary and mental model are in pretty good shape! That means you are ready for the next step, which is to read Max Kuhn and Kjell Johnson's new book [Feature Engineering and Selection: A Practical Approach for Predictive Models](http://www.feat.engineering/)

    <a href="http://www.feat.engineering/" target="_blank"><img src="https://images.tandf.co.uk/common/jackets/amazon/978113807/9781138079229.jpg" width="40%" /></a>

    In my experience, the later chapters in this book filled in a lot of lingering questions I had about certain methods, like whether to use [factor or dummy variables in tree-based models](http://www.feat.engineering/categorical-trees.html). But also don't miss the section on ["important concepts"](http://www.feat.engineering/important-concepts.html) at the beginning- this *should* feel like a nice review if you've gotten this far!


1. [Elements of Statistical Learning](https://web.stanford.edu/~hastie/ElemStatLearn/). The entire PDF of the book is available online. A great resource for those with a strong statistics background, and for those looking for more math and formulas.

## Other note-worthy resources

+ For the highly visual learner, you may want to cue up some YouTube videos from Udacity's ["Machine Learning for Trading"](https://www.youtube.com/playlist?list=PLAwxTw4SYaPnIRwl6rad_mYwEk4Gmj7Mx) course. I found these illustrations especially helpful:

    + [Cross-validation](https://www.youtube.com/watch?v=yBqf9XCpz8o&list=PLAwxTw4SYaPnIRwl6rad_mYwEk4Gmj7Mx&index=187&t=0s)
    + [Overfitting](https://www.youtube.com/watch?v=mfzHchd5La8&list=PLAwxTw4SYaPnIRwl6rad_mYwEk4Gmj7Mx&index=190&t=0s)
    + [Ensemble learners](https://www.youtube.com/watch?v=Un9zObFjBH0&list=PLAwxTw4SYaPnIRwl6rad_mYwEk4Gmj7Mx&index=192&t=0s)
    + [Bootstrap aggregating (bagging)](https://www.youtube.com/watch?v=2Mg8QD0F1dQ&list=PLAwxTw4SYaPnIRwl6rad_mYwEk4Gmj7Mx&index=193&t=0s)
    + [Boosting](https://www.youtube.com/watch?v=GM3CDQfQ4sw&list=PLAwxTw4SYaPnIRwl6rad_mYwEk4Gmj7Mx&index=195&t=0s)
    
    ![](https://i.ytimg.com/vi/Un9zObFjBH0/maxresdefault.jpg)<!-- -->

+ Chris Albon's Machine Learning Flashcards ($12)

    [![](https://d31ezp3r8jwmks.cloudfront.net/variants/BhXYeMJycv8QHBQgJfjemVgz/d2e337a4f6900f8d0798c596eb0607a8e0c2fbddb6a7ab7afcd60009c119d4c7)](https://store.chrisalbon.com/machine-learning-flashcards)<!-- -->

+ [Shirin Elsinghorst's blog](https://www.shirin-glander.de/) (**free! and so good**). 

    <a href="https://www.shirin-glander.de/" target="_blank"><img src="shirin.png" width="1440" /></a>
    
    I love her [sketchnotes](https://shirinsplayground.netlify.com/categories/sketchnotes/).
    
    [![](https://shiring.github.io/netlify_images/lime_sketchnotes_guq6u5.jpg)](https://www.shirin-glander.de/)<!-- -->
    
    
+ I also found Rafael Irizarry's ["Introduction to Machine Learning"](https://rafalab.github.io/dsbook/introduction-to-machine-learning.html), a chapter from his [Introduction to Data Science book](https://rafalab.github.io/dsbook/), to have some helpful discussion.

+ [Machine Learning: A primer](https://www.nature.com/articles/nmeth.4526) by     Danilo Bzdok, Martin Krzywinski & Naomi Altman, from the [Nature Methods Points of Significance collection](https://www.nature.com/collections/qghhqm/pointsofsignificance)- this collection in general is always straight-forward with great visuals. Start with the primer, then skim these:

    + [Statistics versus machine learning](https://www.nature.com/articles/nmeth.4642)
    + [Machine learning: supervised methods](https://www.nature.com/articles/nmeth.4551)
    + [Classification and regression trees](https://www.nature.com/articles/nmeth.4370) (decision trees are the "base learner" for many ensemble methods - this is a good intro)
    + [Ensemble methods: bagging and random forests](https://www.nature.com/articles/nmeth.4438)
    
    ![](https://media.springernature.com/full/springer-static/image/art%3A10.1038%2Fnmeth.4438/MediaObjects/41592_2017_Article_BFnmeth4438_Fig1_HTML.jpg?as=webp)<!-- -->
    

That's all for now- if you are taking my workshop in January I look forward to meeting you in person! If not, rest assured that all code and materials will be shared openly after the workshop. Until then, happy learning 🤖
