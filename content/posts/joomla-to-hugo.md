---
title: "Joomla to Hugo"
date: 2023-04-10T22:57:30-07:00
draft: true
author: "Guy Cutting"
---

![Hugo logo](/hugo-logo.svg)

This post is slightly off topic, but as someone who always likes to peer under the hood when I look at other people's websites, I think some of you might appreciate it. In building this website, I made the decision to leave Joomla behind and embrace Hugo, and I couldn't be happier with the decision.

<br>

For years my business website used Joomla, the open source CMS. I picked Joomla because, after using WordPress for a while, I wanted something with more features and ability to customize. Initially when I started working with Joomla, in about 2015, I was pretty happy with it. It's powerful, supported by all hosting providers, and has a huge ecosystem of extensions, plugins, and templates (themes). But after I managed and developed a Joomla site for a while, I started to grow increasingly frustrated with it. 

<br>

The first problem I found with Joomla was that, despite the huge number of available templates, all Joomla websites sort of end up looking the same. There's a lot of customizability, but a lot of the templates are built on a handful of frameworks, so there's not a lot of genuinely distinctive templates available. 

<br>

Another problem for me is that Joomla is kind of creaky. What I mean is that I felt like I was often running into technical issues that weren't trivial to troubleshoot. More than once a change in PHP version on my hosting provider caused small errors or even broke the site entirely. It's also bloated, since it depends on the whole LAMP stack which includes PHP and MySQL. So even for a small website you have a whole database running in the background and a lot of queries even to build basic pages. 

<br>

That bloat creates a lot of security issues, too. I never had e-commerce or user accounts on my site, so there wasn't much a hacker could do if they gained access, but it was always in the back of my mind that if I was running a site with more sensitive data, Joomla might be a real nightmare.

<br>

Probably my biggest source of frustration related to getting templates to work properly. Some of the first themes I tried weren't easily customizable without a lot of custom CSS, which I'm not proficient at. Eventually I found templates built on the Helix framework, and at first those seemed pretty good. Helix provides a whole graphical interface for customizing your site, so in theory you can easily specify logos, colors, layout, etc.

<br>

I say 'in theory' because as time went on that became increasingly less true. Even in the best case, there was always at least some small set of things that I just couldn't get to look quite right. The site was always about 90% of what I really wanted it to look like. For a while, that was fine, since the site still looked good and functioned well. 

<br>

But I reached a breaking point a few days ago when I was trying to set the site up again after not maintaining it for a while. When I took a full-time salaried job last year, I stopped dealing with the website because I didn't have time and there wasn't much point. So when I decided to start this business, I needed to resurrect it. I thought, 'no big deal, I'll just set hosting up again, install Joomla, and restore the site from a backup.' That process went mostly as planned (despite the always cumbersome process of installing the database and Joomla itself, and reconfiguring some things).

<br>

For some reason, with that last Joomla installation, I hit a template wall. The template I had used for a while would no longer properly reflect appearance and layout changes. I couldn't save changes to colors, fonts, and other things. A lot of the problem, I think, had to do with the big change from Joomla 3 to Joomla 4. That seemed to break a lot of existing extensions and templates that weren't specifically updated for v4, and I read a lot of support threads of other people having similar issues.

<br>

I thought I'd find a different template/framework and ended up installing T4. That was messy because the docs were unclear and even after I had several plugins installed, my chosen template still didn't work right. I finally realized that this situation was never going to get any better, and that I was always going to be frustrated with a Joomla site.

<br>

I had tried Hugo in the past to build a website for a different business. I liked the experience, because it was pretty easy to use but also appealed to my hacker side (using a CLI and working a lot with config files). I decided to give Hugo another go for the rebuild of this website.

<br>

Hugo is a static site generator, meaning that it parses config and markdown files to render your page into static HTML. One of the advantage of this model is speed - when all the server has to do is serve .html pages, it's lightning fast. It also avoids all the issues of database and application configuration. That's not to say that Hugo is a magic wand, since even when you choose a theme, there's still quite a bit of coding-like activity to get the site configured properly and get your content into the right form. 

<br>

The elegant simplicity of having only text files (.html, .css, .toml) on your webserver also is a giant advantage in terms of site reliability. I will never, ever forget the time, a few years back, that my Joomla site broke when my hosting provider did an automatic PHP version upgrade. One day, after not looking at the site for a few days or longer, I visited it to find nothing but a white page with the text 'Internal server error.' That was it. I was in the process of applying for jobs at the time, so I was horrified at the prospect that some potential employer had seen my broken site. For any hiring manager or prospective client evaluating a potential job candidate, seeing a totally barfed site would be an instant dealbreaker. Fortunately I don't think anyone noticed, and after an hour of poking around I figured out the problem and fixed it. But it left me uneasy for a long time to come. But with straight html files, the only thing that could go wrong is if your hosting provider accidentally deleted your files (which is vanishingly rare), or you forgot to pay your hosting bill. The peace of mind of having a rock-solid site that can't break with behind-the-scenes changes on the server is a big plus for Hugo.

<br>

I chose the [LoveIt theme](https://hugoloveit.com/) because I just liked the aesthetics and it had a dark mode (which is huge for me). And it also seemed oriented towards profile-based professional services. It took a few hours of poking around to get the theme configured and adjust a couple of layouts to my needs. But once I got things configured, it's super easy to add content - you just create a new markdown (.md) file and add your content. Hugo renders the markdown into HTML, so it's easy to create visually appealing content without having to deal with HTML or CSS. Hugo also contains a built in preview mode which runs a small webserver on your local machine and automatically rebuilds the site when it detects changes, which makes the iterative process of content creation as easily as it can possibly be. As soon as you save a file, the local server updates the page in your browser, so you see changes as soon as you hit 'save'. And making content changes is also faster because you don't have to wait for a database query for pages to load as you click through a CMS system.

<br>

I spent a few hours tinkering with the configuration, then another few hours building the navigation and putting in the main pages and first few blog posts. Some of this stuff I could copy from the previous site so I saved a bit of time there, but most of the content was original. I'm pretty impressed with being able to build a whole functional website in eight hours. Now I'm **completely** satisfied with the look and feel (which hasn't happened to me in a long time) and just need to add some more social media accounts to the config and I'll be done. From then on, I can just focus on creating content, instead of spending time tweaking small glitches every time I go to add a blog post.

<br>

One of the biggest things I love about Hugo is that there are a lot (several hundred) of [distinctive themes](https://themes.gohugo.io/), and with barely any custom configuration you can get an incredibly crisp, clean looking website. I'm not a graphic designer, so I build websites that have just enough visual pop but are mostly filled with informative text. Hugo is great for this model (though you can use it to build graphics-heavy sites too, if you want). I think the site looks super professional without being overloaded with bells and whistles, which was exactly what I was going for. I find a lot of javascript-heavy websites built in react and other frameworks to be visually overwhelming, and for my needs Hugo strikes a perfect balance.

<br>

While Hugo is a fantastic tool, it's not for everyone or every use case. There are some limitations:
- You can't build whole applications. While you can set up multiple layouts to incorporate a blog or other presentation formats, there's no database for dynamic content. You couldn't run a full-fledged e-commerce site with Hugo, for example. 
- It's not a CMS. While markdown does make it easy to quickly create formatted content, you don't have full WYSIWYG capability for menus or articles. With WordPress or Joomla or other CMS tools, you can maintain a site while knowing nothing about HTML or CSS. Once the site is installed, you can build menus and pages through a visual editor. That's not possible with Hugo. 
- You need a bit of web knowledge to make it work. Related to the above point, Hugo isn't for total web neophytes. While you don't need anything like proficiency with the command line (there's only a couple of commands required to use Hugo), if you're not a bit familiar with the basics of web and comfortable editing config files, you might have a tough time getting started. But if you have even a tiny bit of the hacker in you, Hugo might be right up your alley. And if your web knowledge is basic but you want to learn more, Hugo might be perfect for you.

<br>

So the bottom line is that I can recommend Hugo wholeheartedly. It's not for everyone, but for a lot of use cases it's an amazing solution that avoids a lot of the problems of other website building methods. It's also free, open-source, and has a big ecosystem of users, themes, and support. 

<br>

For my own website needs, it's hard to see going back to Joomla. If I had a web client that wanted a CMS site that would support e-commerce, for example, I might still recommend Joomla (with a few reservations). But for a simple. ultra-clean professional services site with blog support, Hugo is really hard to beat. It's free, and if you have some basic web skills, Hugo makes it insanely easy to quickly build and configure a site and populate it with content. 

<br>

There's always the minor issue of getting your content onto a server, since unlike with a CMS you can't just click the 'save' button in the editor and have the content update on the live site automatically. It's possible to have your website files live in a GitHub or other source control repo and [configure an automated process](https://blog.notmet.net/2020/02/deploying-github-to-dreamhost/) with your web host to upload the changes whenever you push to the repo. If you were doing frequent content updates, you'd probably want to do that. Since I'll probably only be making one new blog post per week or so, for now I'll just stick with the old fashioned method of firing up my FTP client and uploading the new file when I need to make a change. But be aware that you can, with some setup, automate that process.

<br>

Two thumbs up for Hugo! I have never been happier with the appearance and functionality of one of my own professional websites - not even close!. Hugo has made building websites fun again, and that's a great feeling. 