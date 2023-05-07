---
title: "How to Add Utterances Comments Widget to Your Hugo Blog"
date: 2023-05-07
tags: ["Hugo", "GitHub Pages", "Utterances", "Comments", "Tutorial"]
categories:
 - Web Development
 - Blogging
 - GitHub Pages
 - Hugo
 - Tutorials
---

In this blog post, we'll walk through the steps to add the Utterances comments widget to your Hugo-based GitHub Pages site. Utterances is a lightweight, open-source commenting system that uses GitHub issues to store comments.

## Prerequisites

Before we begin, make sure you have:

1. A Hugo-based GitHub Pages site.
2. Installed the [Utterances app](https://github.com/apps/utterances) on your GitHub repository.

## Step 1: Configure Utterances

Visit the [Utterances website](https://utteranc.es/) and configure the widget settings. Copy the generated script, which should look something like this:

```
<script src="https://utteranc.es/client.js"
        repo="your_username/your_repo"
        issue-term="pathname"
        label="utteranc.es"
        theme="preferred-color-scheme"
        crossorigin="anonymous"
        async>
</script>
```

Replace `your_username` and `your_repo` with your GitHub username and repository name, respectively.

## Step 2: Create an Override for the Partial Template

To avoid modifying the theme directly, create an override for the `default.html` partial template in your main site directory:

1. Copy the `default.html` file from `themes/[YOUR_THEME]/layouts/partials/single/` to your main site's `layouts/partials/single/` directory, creating the necessary folders if they don't already exist.

2. Open the copied `default.html` file in your main site's `layouts/partials/single/` directory with a text editor.

## Step 3: Add the Utterances Script

Find an appropriate location within the `default.html` file to add the Utterances script, usually right after the main content area or post metadata (e.g., tags and categories). Paste the Utterances script at that location:

```
<!-- Add the Utterances script below this line -->
<script src="https://utteranc.es/client.js"
        repo="your_username/your_repo"
        issue-term="pathname"
        label="utteranc.es"
        theme="preferred-color-scheme"
        crossorigin="anonymous"
        async>
</script>
```

## Step 4: Test the Integration

Run your site locally using `hugo server` and visit an individual blog post to ensure the Utterances comments widget appears as expected.

## Step 5: Commit and Push Changes

Once the Utterances widget is working correctly on your local setup, commit and push the changes to your GitHub repository:

```
git add layouts/partials/single/default.html
git commit -m "Add Utterances comments widget to blog posts"
git push
```

Wait for the GitHub Actions to build and deploy your site. Visit your GitHub Pages site and navigate to an individual blog post to verify that the Utterances comments widget is functioning as expected.

And that's it! You've successfully added the Utterances comments widget to your Hugo-based GitHub Pages site. Your readers can now leave comments on your blog posts using their GitHub accounts.
