---
comments: true
date: "2015-07-25T22:45:00Z"
tags:
- rust
- totient
- euler
title: Euler's Totient Function in Rust
---

Figured I'd write a much quicker varient of the Totient Function in
Rust. Excellent language. I don't have a grasp on the finer points
available to Rustaceans, but I can hopefully put concurrency and whatnot
to use at some point. The code is quick, but I know it can be quicker if
I just spend some time putting it together.

This is the quick crap I dreamt up:

```rust
use std::env;

fn gcd(mut m: u64, mut n: u64) -> u64 {
   while m != 0 {
       let old_m = m;
       m = n % m;
       n = old_m;
   }
   n
}

fn totient(mut a: u64) -> u64 {
    let mut y = 0;
    let o = a;
    while a != 0 {
        if gcd(o, a) == 1 {
            y += 1;
        }
        a -= 1;
    }
    y
}

fn main() {
    let args: Vec<_> = env::args().collect();
    let n: u64 = args[1].parse::<u64>().unwrap();
    let m: u64 = args[2].parse::<u64>().unwrap();

    let x = (n..m).collect::<Vec<u64>>();

    for i in &x {
        let o = totient(*i);
        println!("{:?}, {:?}", i, o);
    }
    
}
```

The code should compile with no problems. Yes, I realize that u64 is
overkill. No, my code will never require unsigned 2^64 integers. It may
be a quirky choice, but whatever. Change to u32 as needed, though I'm
sure it won't be a problem for anyone.
