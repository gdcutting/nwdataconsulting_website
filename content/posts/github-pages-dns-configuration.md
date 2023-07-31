---
title: "Github Pages Custom Domain DNS Configuration"
date: 2023-07-23T02:37:11-07:00
draft: false
author: "Guy Cutting"
tags: ["GitHub", "DNS", "Hugo", "Domain Management", "ALIAS", "CNAME", "Web", "Cloud"]
---

I'm thrilled to find an [ideal set up for this site](../automated-deployment-githubpages-hugo), which uses GitHub Pages for hosting and GitHub Actions for automated build and deployment. There was one last piece to the puzzle of finally launching the site, and that was configuring the custom DNS with GitHub Pages. When Pages hosts your site, it does so by default at a URL like [https://gdcutting.github.io/nwdataconsulting/](https://gdcutting.github.io/nwdataconsulting/). There's nothing wrong with that URL as-is, but for branding a business, we obviously want a top-level domain that reflects the business name (like [https://www.nwdataconsulting.com](https://www.nwdataconsulting.com)).

So how do we set up a custom domain with a GitHub Pages site? The GitHub Docs are a good place to start (but I'm going to provide a couple of key points of clarification):

[Custom Domains and GitHub Pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages)

That page is a good place to start, and make sure to click through the following docs pages (on managing, verifying, and troubleshooting custom domains). These docs provide everything you need to know to get your custom domain set up, but a key point (the difference between apex domains and subdomains) gets lost in all the verbiage.

The very first thing to do to set up a custom domain is simply to set your custom domain under the 'Custom domain' setting in the Pages section of your GitHub repository settings:

![GitHub Pages custom domain settings](/github-pages-custom-domain.png)

One of the things that the [automated deployment option I'm using ](../automated-deployment-githubpages-hugo) simplifies is further DNS setup for a custom domain. If you're doing your own build (i.e. not using GitHub Actions for deployment), you need to add a CNAME record to your repository, but since we're using GitHub Actions, that's not necessary - GitHub handles everything on its end after you enter you custom domain in the Pages settings. 

The final bits of configuration needed for your custom domain are a couple of DNS record additions. I'm using DreamHost so I'll walk through the process with their DNS management; it should be substantially similar with any other domain name provider. 

The part I want to make clear here is how to handle BOTH the apex domain (nwdataconsulting.com) and the www subdomain (www.nwdataconsulting.com). When we're being casual about it we don't distinguish between the two - but the DNS machinery does in fact distinguish between them, and we need DNS record changes to BOTH of these for the site to be fully accessible. What you'll need for this is:

- an ALIAS record for your apex domain (without the www)
- a CNAME record for your www. subdomain

These records will both point to the same place (gdcutting.github.io for me, or whatever your appropriate URL is for your GitHub username), but they have to be set separately.

Here's how to set the ALIAS record:

![GitHub Pages custom domain settings](/dreamhost-dns-alias-record.png)

And here's how to set the CNAME record:

![GitHub Pages custom domain settings](/dreamhost-dns-cname-record.png)

Notice that the ALIAS record doesn't use the www. subdomain and the CNAME record does (that's the important difference).

GitHub Pages does handle the basic redirect for you (i.e. if you have both apex and subdomains configured in your DNS, Pages will automatically redirect domain.com to www.domain.com). But you still need both DNS records for the site to be fully accessible (otherwise you'll get a network error page on domain.com).

Notice in the above pic of Pages settings that GitHub automatically performs a DNS check on both apex and www subdomains to see if they are configured correctly, and it will give you a big yellow or red warning or error message to let you know if one are both of them aren't configured right.

I was thrown off by the redirect part, because I thought that might be handled on the DreamHost side. It turns out (as the GitHub docs do state, ahem) that GitHub handles this redirect (from nwdataconsulting.com to www.nwdataconsulting.com) for you, but only if you have BOTH the ALIAS and CNAME records set up. 

You can also set up additional subdomains (like blog.nwdataconsulting.com). I'll skip those details here because the GitHub docs linked above do a good job with that. 

Another thing to note (and another perk of using GitHub Pages), is that you get a secure certicate for your site (to make the https:// version accessible and get that oh-so-necessary lock icon in the browser when people visit). You just have to click the 'Enforce HTTPS' box in the Pages settings and GitHub handles this all for you.

That's the last piece of the puzzle to launching the site. Now I have a site that automatically builds and quickly deploys my content changes to my custom subdomain with HTTPS built in. Especially for a free hosting option, it's really hard to beat that. 