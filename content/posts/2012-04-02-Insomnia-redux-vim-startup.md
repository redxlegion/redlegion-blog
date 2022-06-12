---
categories:
- rant
comments: true
date: "2012-04-02T18:20:47Z"
tags:
- rant
- insomnia
- stupidity
title: Insomnia Redux (Or my Excuse to Post my Vim Init)
---

I can't sleep and can't think of anything good to blog about, so I'm going to
throw up my Vim startup script. This is what works for me, and I'm using it with
gvim as well as a slightly modified version for vim. Without further ado, the
startup script that makes the world's best text editor even more useful to me:

{{< highlight vim >}}
colors desert
syntax on
set gfn=PragmataPro:h12,Arial\ Unicode\ MS:h12
set backspace=2
set shm+=I
set ls=2
set ruler

"UTF-8 Shizzle
if has("multi_byte")
  if &termencoding == ""
    let &termencoding = &encoding
  endif
  set encoding=utf-8
  setglobal fileencoding=utf-8
  "setglobal bomb
  set fileencodings=ucs-bom,utf-8,latin1
endif

"Begin custom function for search
highlight found gui=undercurl guibg=#121212 guifg=#6458f0 guisp=#6767ff

function Supafind()
  let farg = input("Search Regex: ")
  call matchadd("found",farg)
  echo ""
endfunction

map <F2> :call Supafind()<CR>
map <F3> :call clearmatches()<CR>:echo "Cleared Matches"<CR>
{{< / highlight >}}
