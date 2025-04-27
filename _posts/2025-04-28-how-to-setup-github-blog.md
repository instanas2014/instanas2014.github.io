---
title: How to setup your personal github blog in minutes?
date: 2025-04-28 03:51:00 +0800
categories: [Other]
tags: [How-To, Github.io, Blog, Setup Guide]
---
Setting up a GitHub blog took me quite a bit of time when I first tried it.  
But if you follow this guide carefully, you can probably have your blog running in just **10 minutes**!

I'm using the amazing **[cotes2020/jekyll-theme-chirpy](https://github.com/cotes2020/jekyll-theme-chirpy)** — a clean, modern, and well-documented template.  
However, there were a few small things that weren’t immediately obvious, so I’ll point them out here to save you some frustration.

---

## Steps to Set Up Your Blog

### 1. Follow the Official Guide

First, head over to the official [Getting Started](https://chirpy.cotes.page/posts/getting-started/) guide from Chirpy.  
It walks you through:

- Creating your GitHub repository
- Setting up your local development environment (I personally used the **Dev Container** approach)

Make sure to follow the steps carefully.

---

### 2. Watch Out for Missing Folders

After setting things up, I noticed some important folders were missing.  
This is briefly mentioned in the `README.md` file generated in your repository — but it’s easy to overlook if you’re rushing.

**The missing folders are:**

- `_data`
- `_includes`
- `_javascript`
- `_layouts`
- `assets`

---

### 3. Additional Steps

To fix the missing folders, do the following:

- **Manually copy** the missing folders and files from the [Chirpy GitHub repository](https://github.com/cotes2020/jekyll-theme-chirpy).

You don't need to copy everything. Some notes:
- In `_data/locales`, I only copied over `en.yml`.
- In `_includes/analytics`, I only included `google.html`.

Feel free to adjust based on your needs.

---

### 4. Update Configuration Files

After copying everything, update the following files to personalize your blog:

- `_data/authors.yml`
- `_data/contact.yml`
- `_config.yml`

These files control your site's metadata, author information, and settings.

---

### 5. Customize Your Favicon

Next, update your site's favicon to make it truly yours.  
Follow the [favicon customization guide](https://chirpy.cotes.page/posts/customize-the-favicon/) provided by Chirpy.

---

### 6. Set Up Comments

To enable commenting on your blog, follow this great [guide from Patrick Thurmond](https://www.patrickthurmond.com/blog/2023/12/11/commenting-is-available-now-thanks-to-giscus).

Here's a quick summary:
- Go to [giscus.app](https://giscus.app) to generate the configuration.
- From the generated JavaScript snippet, copy the value from:
  - `data-repo`
  - `data-repo-id`
  - `data-category`
  - `data-category-id`
- Update these values under the `comments` section in your `_config.yml`.

---

## Done! 🎉

That's it!  
Your personal blog is now live at `https://your-github-username.github.io`.

Enjoy blogging!
