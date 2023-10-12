---
title: "Code Blocks Syntax Highlights"
date: 2023-08-01T14:57:29-07:00
draft: true
author: "Guy Cutting"
tags: ["Web", "Hugo", "GitHub", "Markdown"]
Categories: ["In Practice"]
---

I've really been enjoying developing this new website, learning some new tools and skills and getting a chance to work in more depth with some that I had already used in the past. I've posted a few articles discussing the process of developing and deploying the site, because even though that discussion is a little off-topic from my data consulting work proper, I think there are others like me who might find some of this information useful. Though I'm not primarily a web developer anymore, I spend over a decade building websites for a living, and I still really enjoy doing it. In fact, I think I enjoy building sites *more* now because, since it's not my primary job, I can focus more on getting exactly what I (instead of my web clients) want out of the site, and I have a chance to try to things that I wouldn't if I was filling orders for clients. 

There are a lot of people like myself who want to get content out on the web but aren't professional developers, and need an easy (but still powerful) set of tools for building sites and publishing content. There are so many tools available for web development, and it's a great time for those of use who don't have time to specialize in HTML/CSS/javascript/react or to get into the weeds of hosting and deployment. I've never been totally thrilled with CMS systems like WordPress, though they do have a place
## GitHub Is The Standard For Displaying Code On The Web

One of the great things about [GitHub](https://github.com/) is its many built-in features for working with code, among them displaying code blocks, language-aware syntax highlighting, and the like. GitHub, because its *raison d'etre* is storing and displaying people's code, pioneered a lot of these features in order to provide an intuitive and informative code-viewing experience. Things like colored code blocks with a separate font, highlighting, and line numbers make it immediately obvious what's code and what's not, and make it easy to navigate code (just like the experience in a modern IDE). So for a programmer and data practicioner like myself, these code-related features have become an essential feature of any working and display environment, including my own website.

[put in small pic of github code display]

If you haven't noticed, this site is built consciously to look like GitHub, in part because of the choice of theme - [LoveIt](https://themes.gohugo.io/themes/loveit/), by Dillon (great work, Dillon!). Particularly with the dark version of the LoveIt theme (click at the top right of any page to switch between light and dark modes), the site resembles GitHub with its grey-on-grey theme (which I'm obviously a big fan of). Part of the reason for that appearance choice, which hopefully makes people think of GitHub, is that this site is text- and code-focused, rather than being heavily graphical. I'm a data developer working almost exclusively on the backend, and graphical and front-end web design are not among my skills. So I wanted a choice of theme that would look good with large amounts of text and minimal graphics (which, for better or worse, is the world I work in, and I want the site to convey that). The LoveIt theme struck me immediately because of its clean lines and minimalist (yet still attractive) and highly functional appearance.

## Hugo's Built-In Code Display Features

One of my favorite features of Hugo, and a significant factor in deciding to use Hugo for this site (as opposed to WordPress or some other CMS) is that it also includes a number of code-display related features, and other features (like the use of Markdown) which are similar to Github and reproduce the GitHub experience. Even at first glance its obvious that this site is focused on code, and Hugo's built-in features are a big source of its appeal for me (and a lot of other developers):

[link to Hugo docs discussing code features]

### Hugo vs WordPress and Joomla

Hugo's functionality with code display was one of the major deciding factors in using it to design this site, but the decision (as compared to WordPress or another CMS) wasn't entirely obvious. I used Joomla for my personal and business websites for years, and also have a lot of experience with WordPress. Both of these platforms offer code-display features that integrate with their visual editors. The basic code blocks are pretty minimal, and not terribly attractive, but are a good place to start. Coupled with third-party plugins like [prism.js], they offer WordPress and Joomla developers their own set of tools for working with code. 

The previous version of my business website, which focused more on systems science, also had a lot of code-related content, and I found a couple of plugins that let me make the code display more attractive and easier to navigate. But like a lot of other things with Joomla, I felt like I could never get this aspect of the site quite right. I used code blocks with syntax highlighting and some other features, but I could never quite get them to look like GitHub, which is my perennial standard for what code should look like on a website. So when making design decisions about this website, I was already inclined away from using a CMS, since I had encountered limitations when using them for pages and posts containing code blocks.

## What Hugo Offers

...

A big similarity between Hugo and GitHub is that they both use [Markdown] for marking up content. This one perhaps the feature that sold me on Hugo first - after becoming familiar with GitHub from posting my code there, I realized the flexibility and power of markdown. I have some HTML experience from earlier in my web career, but I've never been a front-end developer, and I know very little CSS. With enough Googling, I can usually find a working solution for small HTML/css things that I'm trying to do, but I'm by no means a front-end developer, so for more robust functionality I rely on packaged solutions that other people and projects have developed. 

GitHub has popularized the use of Markdown because it's such a good solution to the problem I'm describing. I want to create attractive, well-organized web content, but don't know much modern HTML and CSS, and I'm moving away from using CMS systems with their visual editors. Markdown is brilliant because it's lightweight, easy to learn, and provides the most important markup features available in HTML and CSS (like links, images, headers, lists, tables, etc.). A person with no knowledge of web development can learn enough markdown in five minutes to get started making content, and with a [cheat sheet] by your side, you can quickly figure out how to do anything markdown allows. 