---
layout: post
title: Moving Blog Engines - from Ghost and Azure to Jekyll and GitHub Pages
---

## Synopsis

Looking for an even easier (and cheaper) way to host and keep my blog up to date, I migrated from [Ghost](https://ghost.org) 
hosted on my personal [Azure](https://azure.microsoft.com) subscription to [Jekyll](https://jekyllrb.com) and 
[GitHub Pages](https://pages.github.com). So far, I've been very impressed with the ease of use and overall 
configurability of Jekyll, not to mention no more hosting costs! I describe the process below, in case anyone else is 
looking to do the same.

## Background

> [Skip ahead](#steps) to the juicy details if you're not interested in the motivation or background for this post :-)

I started this blog back in 2008 using a hosted [WordPress](https://wordpress.com) site and although I'm far from being
a prolific blogger, it has served to scratch the occasional typing itch while hopefully helping the odd person solve a 
particular problem I had battled through myself. I later moved to hosting my own instance of WordPress on the then 
fledgling [Azure App Services](https://azure.microsoft.com/en-us/services/app-service), but the speed (on the lower cost
plans anyway) was abysmal and I sought something a bit more lightweight.

The Ghost blogging engine had just been released around this time (circa 2014) and seemed to be the perfect platform, 
one that put the actual writing of content front and centre. It was clearly aimed at developers and / or a more 
technical audience, given the installation and deployment involved cloning their repo from github, setting up your own
config and publishing to your website. 

There were a few little idiosyncrasies to get this working on Azure at the time given it was a Node app while .NET was
the preferred platform on Azure, with some PHP and Java support back then, although I'd imagine this improved over time.

A forked Ghost repo was put together by [Felix Rieseberg](https://github.com/felixrieseberg/Ghost-Azure) with everything
setup and configured correctly for Azure, and this was the version I ended up using.

My blog ticked along nicely for a few years, and to be honest, with a hectic work and life schedule, I was rarely
finding the time to write much anyway. 

So why the sudden change to Jekyll and GitHub Pages? Glad you asked! It was prompted by a couple of things: First, even
though Ghost made it incredibly simple to start writing content and supports markdown, just the physical act of logging
into the admin site and creating a new page was often enough of a blocker for me not to start to write something.
What I _really_ wanted was a local solution, preferably markdown based and backed by a github repo that I could pull
from anywhere, start writing notes and ideas in a local editor of my choice (e.g. vim) and easily publish them when I
was ready.

The other catalyst was that I wanted to get my Ghost install updated, but by being on the custom azure repo and not the
main version, I would have to reintroduce a couple of (admittedly small) changes such as Google Analytics and Disqus
comments. It felt like a bit of a chore every time I wanted to update my Ghost version, as I'd need to get my head
around the content database, config, repo versions, Azure Node config etc etc. This is not a criticism of Ghost at all,
but more pointed to the fact I wanted as low friction solution as possible.

My first thought (being a developer) was that I could I write something to achieve this simple and minimalistic
workflow. While it's always nice to have a side project to try new ideas out, usually the more sensible thing to do is
see if there was a solution already. I felt a static-site generator was going to be the way to go, so started looking
into these. Being predominately in the [.NET](https://dot.net) space, I had a quick look into ASP.NET specific site
generators, the most promising of which (at least to me) seemed to be [Wyam](https://wyam.io/).

All this searching around static site generators inevitably brought up Jekyll as an option, but it was the option to use
it with GitHub Pages that piqued my interest. I'd certainly heard of Jekyll before, although I couldn't have told you
much about it other than the fact it was a static site generator! Was this an easy route to my magical combination of
Markdown + local editing + a git repo? The answer of course was emphatic "yes!", and after spending a couple of hours
getting everything migrated across and redirects in place, what better way to celebrate than by writing up a description
of the process to give my new workflow a whirl. So far, so good as I'm typing this locally in WebStorm with the Markdown
Support and IdeaVim plugins, after which I will push the git repo and as if by magic, the post will be published. Ah,
bliss... oh, and as a bonus change, I also took the opportunity to move to my new [daniellewis.dev](https://daniellewis.dev)
domain and added https support with the click of a button in GitHub pages settings... noice!

## <a name="steps"></a>Steps

> All steps below are based on my experience with macOS Mojave (10.14)

* [Create a GitHub Pages repo](#create)
* [Install Jekyll and Bundler](#install)
* [Import your old Ghost posts and content](#import)
* [Site config, Google Analytics and Disqus comment support](#config)
* [Add, commit, push!](#git)
* [Bonus - custom domain, https and redirects](#bonus)

### <a name="create"></a>Create a GitHub Pages repo

Following the very simple steps on [GitHub Pages](https://pages.github.com), create a user-id.github.io repo using
the name of your github account e.g. `djjlewis.github.io`.

Once created, `git clone` this to a local directory e.g. `~/github-pages/djjlewis.github.io`

### <a name="install"></a>Install Jekyll and Bundler

Jekyll is written in Ruby, so it goes without saying that you will need Ruby installed. Ruby is bundled with macOS but 
Jekyll requires a more up to date version (>= 2.4.0) than ships with Mojave (2.3.0). I'd recommend installing [brew](https://brew.sh)
and then doing `brew install ruby` to make sure you have the latest.

Once installed, make sure the path to the new ruby comes earlier than the `/usr/bin` OS version. You can easily check by
typing `which ruby` and checking it is in `usr/local/opt/ruby/bin/ruby`.

The [Jekyll documentation](https://jekyllrb.com/docs/) is fantastic, so I won't recreate here for no reason. Just follow
the [macOS installation guide](https://jekyllrb.com/docs/installation/macos/) to the letter and note you will **very likely 
need to make two modifications to your path in `.bash_profile`**.

`cd` into your recently cloned github pages repo tun `jekyll new .` to install it locally. You could do a 
`git add . && git commit -m "Initial commit"` now in case you want to go back at any point to fresh copy.

> Note: Some earlier Jekyll articles and blog posts will talk about modifying files in the _includes directory and so
> on. In later versions of Jekyll, these files are included separately as part of the template, so in most cases you
> will not see them in the director structure by default. It is possible to add and override these template files, but
> that is not the objective for today.

### <a name="import"></a>Import your old Ghost posts and assets

This will vary a little depending on how and where you host Ghost and which version you are on. In my case, I logged
into the Ghost admin (`[ghost-blog-url]/ghost`), Labs menu, and then Export, which will download a json file containing
all your posts including the content, tags, author information etc. 

If you have any images in your Ghost content directory, copy this under your new Jekyll directory e.g. 
`/djjlewis.github.io/content/images/[201x]`. The will be picked up automatically from the links in the exported Markdown
when you generate the Jekyll site.

The next step is to install the [Jekyll Ghost importer Gem](https://github.com/eloyesp/jekyll_ghost_importer). Follow
the instructions on the github page and you will have nicely populated `_posts` and `_drafts` (if applicable) 
subdirectories in your main Jekyll directory.

### <a name="config"></a>Site Config, Google Analytics and Disqus comment support

You'll want to edit `_config.yml` and provide some sensible defaults which should all be fairly self-explanatory. In my
case, I wanted to match the URLs of my old ghost site in order to keep what little Google SEO I may have, so went with
`permalink: pretty` which will produce `/year-month-day-title/` URLs and strip the `.html` prefix which is on by default.

The default theme for Jekyll, [Minima](https://github.com/jekyll/minima), includes support for Google Analytics and
Disqus comments out-of-the-box. Just add the following additional config values:

```yaml
google_analytics: UA-xxxxxxxx-x
disqus:
  shortname: [disqus_short_name]
```

### <a name="git"></a>Add, commit, push!

And that's it... after a quick local test (note that the GA and Disqus features are disabled when running locally) and a
couple of git commands later, the new site was converted and published to Github Pages as a statically generated site
using Jekyll, along with all the content, same URL structure, images, GA and Disqus support I had on the old blog.

### <a name="bonus"></a>Bonus - custom domain, https and redirects

As mentioned, I also took this opportunity to move off my old `.me.uk` TLD and onto my shiny new `daniellewis.dev`
domain.

The first step is to ensure a `CNAME` or `A` record has been set up in your DNS providers management area. Follow the 
steps outlined in [Setting up a custom domain](https://help.github.com/en/articles/quick-start-setting-up-a-custom-domain).

Once that is in place, you can configure your custom domain via the Github Pages repo Settings area or just add a new
file to your local repo called `CNAME` with a single line containing your custom URL. If the DNS settings are configured
correctly, you should also be able to flip the `Enforce HTTPS` option and get TLS for free as GitHub pages will use a
free certificate generated by [Let's Encrypt](https://letsencrypt.org/).

More info on how the custom domains are available on these blog posts [Free SSL with a custom domain on GitHub Pages](https://bart.degoe.de/free-ssl-on-github-pages-with-a-custom-domain/) and
[GitHub Pages and Let's Encrypt](https://bart.degoe.de/github-pages-and-lets-encrypt/)/.

For redirects, the quickest option for me (for now) as I was hosting on Azure was to add a `web.config` file into the
`wwwwroor` folder of the app service with a simple redirect:

```xml
<?xml version="1.0" encoding="utf-8"?> 
<configuration> 
    <system.webServer> 
        <httpRedirect enabled="true" 
                      destination="https://daniellewis.dev" 
                      httpResponseStatus="Permanent"/> 
    </system.webServer> 
</configuration>
``` 

> source: [Azure Tip — just a Web App with redirect please](https://michelebusta.com/azure-tip-just-a-web-app-with-redirect-please-a045d1072659)

## Conclusion

So there we go, a couple of hours work or so, and I finally have complete control over not only my blog content (simple
markdown files on disk), how I publish (push to remote git repo) but also full and complete control of the layout using
Jekyll's very simple templating language. Although I'm on the default theme for now, I anticipate writing my own layout
soon so I can try out some newer CSS layout techniques (specifically Grid and Flexbox) but also because I want to try
writing some more long term technical guides which will sit outside the normal blog style of chronological posts.

Please leave a comment below with any feedback or suggestions and hopefully content will be a bit more forthcoming
in the weeks and months to come. Stay tuned!