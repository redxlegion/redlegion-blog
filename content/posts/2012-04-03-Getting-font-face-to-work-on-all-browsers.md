---
comments: true
date: "2012-04-03T14:37:27Z"
tags:
- css
- html
- web
- info
title: Getting @font-face to Work on all Browsers
---

I've tried probably about ten suggestions found all over the web, and this is
the only method I've found to function universally, across every browser I've
tested it with.

{{< highlight css >}}
@font-face {
    font-family: 'NameOfFontFamily';
    src: url('/font/file.eot?') format('eot'),
    url('/font/file.woff') format('woff'),
    url('/font/file.ttf') format('truetype');
}
{{< / highlight >}}

You can use online font converters to convert an OpenType or TrueType font to
*.eot and *.woff as needed. For whatever reason, the "?" appears to be important
as well. Not sure about that, I'll have to look into it further.
