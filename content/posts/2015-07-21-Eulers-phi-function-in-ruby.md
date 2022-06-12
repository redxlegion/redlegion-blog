---
comments: true
date: "2015-07-21T13:04:00Z"
tags:
- ruby
- euler
- wat
title: Euler's Phi Function in Ruby
---

I've taken a few implementations apart and I've tried to figure out what
the intention of Euler's Phi function is. I think I've got it. I found
an interesting implementation in Ruby
[here](https://github.com/gmarik/99problems/blob/master/Ruby/arithmetic.rb)
but it wasn't satisfactory. Sure, the code was incredibly minimalistic,
but it was also recursive and overflowed the stack for anything over
7704 iterations. I didn't like the inflexibility of it. So I rewrote it
in big ugly moron code that isn't recursive, but is capable of scaling
to some decently large totients. I might see if I can code something
similar in Rust, just for shits and giggles.

By the way, the output makes for some damned interesting graphs.

{{< highlight ruby >}}
# encoding: UTF-8

usage = <<ELSTRINGSTART
USAGE:
totienttest.rb <start> <end>

<start> is the number you want to begin at. (Duh.)
<end> is where you expect to stop. (Fucking retard.)
ELSTRINGSTART

def totient_phi_new(n)
    c = 0
    n.downto(1) { |x|
        if x.gcd(n) == 1
            c += 1
        end
    }
    c
end

if ARGV.empty?
    puts usage
    exit
end

if ARGV.length > 2 or ARGV.length == 1
    puts usage
    exit
end

x = ARGV[0].to_i
y = ARGV[1].to_i

x.upto(y) do |t|
    puts "#{t}, #{totient_phi_new(t)}"
end
{{< / highlight >}}

I'm such a fucking brocoder. Eugh.

![Totient](/img/2015/totient/graph.png)
