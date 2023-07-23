---
title: "Automated Hugo Deployment using GitHub Pages"
date: 2023-07-19T19:12:11-07:00
draft: false
---

I finally got this site into shape with the theme ([LoveIt](https://github.com/dillonzq/LoveIt)) chosen and configured. One of the few issues that I have with Hugo is the lack of theme standardization. There's not a lot of standardization enforced on theme developers, so there's a very wide range of theme setups and configurations out there. As a result, theme testing can be onerous when you're working on a new site. One of the really nice things about WordPress is that (since theme standardization *is* heavily enforced), changing themes is as easily as adding and activating the theme in the admin interface (which just requires a few clicks). With Hugo, you have to download the theme manually, decide whether or not to add the new theme as a Hugo module or git submodule, then figure out where in the theme configuration the options that are most important to you live. Sometimes the theme doesn't work right out of the box, and you get a broken site and have to dig around to figure out the configuration change that will get you a properly working base configuration before you can even check out how the theme looks with your content and start to play with the options. This is by far the thing that I like least about the development cycle with Hugo, and unfortunately there's no way around it, because the lack of theme standardization is at this point baked into how the project is run.

But once you choose a theme (which usually requires several rounds of the process described above, since for each candidate theme for your new site you at least have to do some downloading and basic setup, and usually on top of that you have to do some troubleshooting for a broken initial setup), the development cycle becomes a lot easier. At that point, when you're adding your own content and working with the templating engine, you're in more clearly mapped territory where there's less room for confusion. Creating content obviously depends on you and not a theme developer, and the templating is thoroughly documented within the Hugo project (unlike themes). So now I'm at the point where I'm past the worst of the hassle and can just focus on the fun part, which is making content. But there's one more issue to solve, and its an important one to get right since it will determine whether the site is easy to maintain and update in the future. That issue is how to deploy the site. The least technical way probably is to run Hugo local every time there are changes, then just upload the newly rendered .html files to a web server. I have a Dreamhost account, and I could use it for this deployment, but I was interested in using [GitHub Pages](https://pages.github.com/), partly to learn more about it and partly because my Dreamhost plan only includes one hosted site, and I can get the site hosted for free with Pages.

With Pages, there's more than one way to handle the deployment. From what I can tell, there are three in fact:

- as described above, run Hugo locally to render content additions/updates, and then manually push the files to GitHub (either using CLI git or through the GitHub web interface.) This method works fine but doesn't take advantage of all the GitHub features that are available. 
- the second method (see pick below) is to use GitHub's automated deployment feature to deploy a static site. With this option, I still have to build the site locally (by running Hugo to render the new content and config changes). I'm not honestly sure why you'd use this option, since if you're doing the Hugo build locally, the only thing left to do is to transfer the files to GitHub servers, which will happen automatically when you do whatever git workflow (CLI, through a VS Code extension, etc.) you do. GitHub Pages serves out of your repo, so once the files get updated there's nothing else to update. If someone wants to fill me in on why you'd want to use this method, feel free. Maybe I'm missing something.
- the third and pretty clearly best method is to use GitHub automated deployment option with the remote Hugo build. With this method, once you push your files to the repo, GitHub performs the Hugo build automatically and your site gets updated with the new content. This makes it super easy to do content changes. My standard git workflow (I find myself still using CLI most of the time because it is faster) looks like:

```bash
git add -A
git commit -m 'my commit message'
git pull 
git push
```

which stages changes, performs the commit, pulls down changes from the remote repo, and pushes local changes to the remote. This just takes a few seconds, and once you do this, everything else (the Hugo build and site update) happens (mostly) behind the scenes on the GitHub side, using GitHub Actions.

Here's a shot of the repo settings GitHub Pages section showing the second two deployment options discussed above:
![GitHub Pages deployment options for Hugo site](/nwdataconsulting/github-pages-deploy-options.png)

There's a bit of infrastructure-as-code that GitHub uses to handle these automated deployments - a .yaml file that lives in your directory and gives build parameters such as Hugo version, OS version, which branch to build from, etc:

![GitHub workflow file for Pages site build](/nwdataconsulting/github-deploy-workflow-file.png)

Most of this is boilerplate and you don't need to worry about changing it, but it is interesting to look under the hood to glean some info about how these builds are performed. When you select one of the above two Pages deployment options (Hugo build or static site), GitHub automatically generates this .yaml workflow file for you, so you don't have to know any of the details. The only thing you'll probably want to check is the build branch, because if you're not using `main` then you'll want to specify that near the top with the `branches` parameter.

Now that we've got the automation workflow set up. What happens when we run it, which happens automatically when any changes to the build bras1s1nch (in my case `my-pages`)? One of the great things about GitHub is that it has all sorts of fancy machinery (hooks on the backend and JS on the front) to detect changes and display status in real time. When you trigger the build, the 