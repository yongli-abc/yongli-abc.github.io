---
title: "Adding a Read Time Estimation to Your Hugo Blog Posts"
date: 2023-05-09
categories: ["Hugo", "Web Development", "Blogging"]
tags: ["hugo", "blogging", "read time", "web development", "static site generators"]
---

In this blog post, we're going to learn how to add a read time estimation to your Hugo blog posts. This is a useful feature to let your readers know approximately how long it will take to read your content.

Firstly, navigate to the layout where you want to add the read time. This is typically in a file like `layouts/posts/single.html` or `layouts/_default/single.html`, depending on your theme and setup.

Add the following code to the location in the HTML where you want the read time to appear:

```html
<p>Read time: {{ div (countwords .Content) 200 }} minutes</p>
```

In this code, .Content is the variable that contains the content of your post, countwords is a Hugo function that counts the number of words, and div divides the word count by 200 to give an estimated read time in minutes.

If you want to round the read time to the nearest whole number, you can use the math.Round function like this:

```html
<p>Read time: {{ math.Round (div (countwords .Content) 200) }} minutes</p>
```

To include the read time in your post list, modify the template file that generates the list of posts, typically located at layouts/_default/list.html or layouts/posts/list.html.

Assuming you have a loop structure that iterates over the posts, add the read time calculation within that loop:

```
{{ range .Paginator.Pages }}
  <article>
    <h2><a href="{{ .Permalink }}">{{ .Title }}</a></h2>
    <p>{{ .Summary }}</p>
    <p>Read time: {{ math.Round (div (countwords .Content) 200) }} minutes</p>
  </article>
{{ end }}
```

Don't forget to save your changes and rebuild your site to see the updated read times on your posts.

Now you can easily provide your readers with an estimate of how long it will take to read your posts, enhancing the user experience on your blog.