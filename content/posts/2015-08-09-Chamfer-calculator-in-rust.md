---
comments: true
date: "2015-08-09T00:00:00Z"
tags:
- machining
- rust
- chamfer
- calculator
title: Chamfer Calculator in Rust
---

I'm going to go through my old TI-82 calculator and rewrite my most
useful little trig tidbits in Rust for everyone to use. The first one
I'm going to reiterate will be my chamfer calculator. This is pretty
handy if you ever have to measure chamfer diameters in a production
environment. You can quickly calculate the greatest diameter of any
given print dimension chamfer with this tool. It ought to compile on the
latest version of Rust without warning. Should. I've hit my Ballmer
curve, so I'll just throw that warning right away.

Here goes.

{{< highlight rust >}}
use std::io;

fn chamf(d: f64, a: f64, b: f64) -> f64 {
    ((a.to_radians().tan() * d) * 2.0) + b
}

fn seek(p: &str) -> f64 {
    let mut buffer = String::new();
    println!("\n{}", p);
    io::stdin().read_line(&mut buffer)
               .ok()
               .expect("Failed to read line!");
    buffer.trim().parse::<f64>()
                 .ok()
                 .expect("Not a float!")
}

fn main() {
    let x = seek("Enter Min Depth: ");

    let y = seek("Enter Min Angle: ");

    let z = seek("Enter Min Bore: ");

    let i = seek("Enter Max Depth: ");

    let j = seek("Enter Max Angle: ");

    let k = seek("Enter Max Bore: ");

    println!("\nMin Result:\n{} mm\n{} in", chamf(x, y, z), chamf(x, y, z)/25.4); 
    println!("\nMax Result:\n{} mm\n{} in", chamf(i, j, k), chamf(i, j, k)/25.4);
}
{{< / highlight >}}

So, yeah. No comments. If you can't read it, you shouldn't bother. It's
supposed to be human-readable, dumbass.

Have fun.

_**EDIT:**_ Changed the code a bit. Made it better. Don't judge me.
