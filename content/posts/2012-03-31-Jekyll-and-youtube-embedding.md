---
comments: true
date: "2012-03-31T04:19:13Z"
categories:
- blogging
tags:
- jekyll
- youtube
- embed
- video
title: Jekyll and Youtube Embedding
---

When I first began using Jekyll, I noticed that throwing in a Youtube embedded
video made it go apeshit. I Googled for a bit to discover that Maruku wasn't
happy with HTML, and was taking any and all HTML and interpreting it to XHTML.
Youtube doesn't provide "Embed" data in XHTML format. Here is an example of a
typical Youtube embed:

{{< highlight html >}}
<iframe width="420" height="315" src="http://www.youtube.com/embed/dQw4w9WgXcQ" 
        frameborder="0" allowfullscreen></iframe>
{{< / highlight >}}

That's taken verbatim from Youtube. There are two problems here. First, XHTML
doesn't like lone attributes. The `allowfullscreen` attribute has to be changed
to `allowfullscreen="allowfullscreen"` to be usable. If you even use it.
I've heard reports of people embedding videos without it at all. Second, Jekyll
devs openly admit [Jekyll swallows empty end
tags](https://github.com/mojombo/jekyll/wiki/Markup-Problems). Thankfully, their
admission gleans a helpful hint in fixing it. Simply insert a space between
`<iframe>` and `</iframe>`. The end result is as such:

{{< highlight html >}}
<iframe width="420" height="315" src="http://www.youtube.com/embed/dQw4w9WgXcQ"
        frameborder="0" allowfullscreen="allowfullscreen">  </iframe>
{{< / highlight >}}

The above code will embed properly and report no issues with Maruku. Have fun.

---Nevermind. "Allowfullscreen" isn't an allowable attribute. Just dump it entirely.
