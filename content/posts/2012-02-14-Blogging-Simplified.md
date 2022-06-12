---
date: "2012-02-14T18:08:00Z"
tags:
- tech
- jekyll
title: Blogging Simplified
---

[Jekyll](https://github.com/mojombo/jekyll/wiki) is an excellent *"simple, blog
aware, static site generator"*. It allows you to use special shorthand syntax
like [Textile](http://en.wikipedia.org/wiki/Textile_markup_language),
[Maruku](http://maruku.rubyforge.org/maruku.html), or other markup syntaxes to
quickly and easily generate static blog content. The resources available on the
internet for using Jekyll to blog are downright plentiful, and the tool itself
is incredibly flexible.

The first thing you'll have to do is grab a Jekyll layout from a current Jekyll
blog. They're all over the place, and nearly every one I've seen has been
excellent. Choose what looks good to you. The markup supported is so easy that
you can manually edit each layout easily to make it suit your own requirements.
You'll also find a plethora of information on how to include Disqus and other
features you may require for your blog. Make it as complex or simple as you
please. The nice thing is that you're less likely to experience server-side
scripting problems, since the platform generates static HTML. No SQL or PHP
locking down required. Just generate your content and you're good to go.

I'll just leave you with one quick tip: Make sure your blog posts include the
"date:" YAML tag. It makes blog post sorting accurate, whereas the filename-only
syntax for posts doesn't always display them in proper order. The format for the
"date:" YAML tag is as such:

    %Y-%m-%d %H:%M

Well, that's all I can think of for the moment. If you have questions or would
like me to help you get your Jekyll-based stuff set up, just shoot me an email.
I'm pretty much always happy to help. <redlegion@gmail.com>
