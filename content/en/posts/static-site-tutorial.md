---
title: "A tutorial to create static websites (kind of)"
date: 2025-03-03
draft: false
---

(You can read [this post in Spanish](valenvilardav.blog/es/posts/static-site-tutorial))

Creating a static website should be easy. And it is. In this post, I’ll show how I created the blog you're reading. 

<!--more-->

# Intro

To understand the decisions I made, a good starting point is knowing my requirements.  
I wanted a blog that met the following criteria (in order of importance):  

1. Its cost had to be 0.  
2. It had to be easy to set up and maintain.  
3. It had to be visually appealing.  
4. I wanted to gather metrics about my site.  

# Technology Definition

When thinking about a static blog, the first thing that likely comes to mind is [GitHub Pages](https://pages.github.com/). This service lets you create and host static websites for free. You simply upload your code to a public repository, enable GitHub Pages, and your site will be available on the internet. Perfect, points 1 and 2 are covered.  

However, GitHub Pages doesn't provide a way to view metrics "out of the box," as shown in this [discussion](https://github.com/orgs/community/discussions/31474). This is where [Cloudflare Pages](https://pages.cloudflare.com/) comes in. It offers the same benefits as GitHub Pages, plus additional features [for free](https://www.cloudflare.com/plans/developer-platform/), including a very comprehensive web analytics dashboard.  

Now, points 1, 2, and 4 are met. What about point 3? Well, early in my research, the first tool I found to generate static sites was [Jekyll](https://jekyllrb.com/), a static site generator that uses templates to turn Markdown files into visually appealing websites.  

But, I didn’t stop there. I kept searching and found [Hugo](https://gohugo.io/), another static site generator with similar features. Personally, I didn’t find one significantly better than the other, and ultimately, I chose Hugo. You can read a great comparison in this [post](https://draft.dev/learn/hugo-vs-jekyll)  

# Implementation Steps

1. **Create the repository:** You can use GitHub or GitLab, and it can be either public or private. In my case, I created a [public repository](https://github.com/valenvilardav/blog) on GitHub where you can view the code used for this blog.  

2. **Create the new site:** Use the `hugo new site` command to create the directory structure, then install a theme by following the documentation, and finally push everything to the new repository.  

3. **Integrate with Cloudflare Pages:** To create a new page, go to Cloudflare, and in the "Workers & Pages" section, create a new application. To do this, connect Cloudflare with your version control tool. For GitHub, you only need to install an [app](https://docs.github.com/en/apps/overview) and grant it permission to access the specified repository.  

4. **Build and deployment configuration:** This part is straightforward. You can use a [preset](https://developers.cloudflare.com/pages/configuration/build-configuration/) for your chosen language. In my case, the theme requires installing a dependency with npm, so my build command is `npm install && hugo`.  

   One important note is to set the Hugo and Node versions using the `HUGO_VERSION` and `NODE_VERSION` variables, respectively. Otherwise, default older versions will be used, which can lead to issues.  

5. **Accessing the site:** Once set up, you can visit your site at the domain provided by Cloudflare.  

## What if I want to configure a custom domain?

To do this, you need to manage your domain through Cloudflare. In my case, I purchased it from Hostinger, so I had to change the NS records to use Cloudflare’s. Then, simply add a [custom domain](https://developers.cloudflare.com/pages/configuration/custom-domains/) to your page.  
