---
title: "Fixing CORS Issues on a GitHub Pages-hosted Hugo Site"
date: 2023-05-07
draft: false
tags:
  - GitHub Pages
  - Hugo
  - CORS
  - Web Development
categories:
  - Web Development
  - Blogging
  - Hugo
---

Recently, I encountered a CORS issue with my personal blog site hosted on GitHub Pages with Hugo. After purchasing a custom domain from GoDaddy and setting up an SSL certificate, my site only displayed the HTML content, and all the CSS styling was missing.

Upon investigating the issue, I found that the browser was blocking the CSS resources due to the "integrity" attribute in the link tag. This attribute is used to ensure the integrity of the requested resource, but it requires CORS to be enabled.

To fix this issue, I followed these steps:

1. Removed the "integrity" attribute from the link tag for the CSS file.
2. Added a `.nojekyll` file in the root of my repository to disable Jekyll and configure CORS.
3. Created a `_headers` file in the `static` folder of my Hugo project to add CORS headers.
4. Added the following lines to the `_headers` file to enable CORS for my CSS files:

```
/*.css
Access-Control-Allow-Origin: *
```

5. Committed and pushed the changes to my GitHub repository, and GitHub Pages served the CSS files with the required CORS headers.

After following these steps, my site displayed correctly with all the CSS styling intact. I hope this solution helps anyone facing a similar issue with their GitHub Pages-hosted Hugo site. Happy blogging!
