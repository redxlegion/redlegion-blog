---
comments: true
date: "2016-02-28T14:12:00Z"
categories: 
- info
tags:
- c
- euler
- totient
title: Totient Calculator in C
---

Rewrote my totient calculator in C. It's pretty much a direct
translation of the excrement I wrote in Rust. Be gentle, there are
obvious points that I miss completely in C that veterans in the
ancient language would scoff heartily about. I don't yet know what the
hell a struct is for or the extents of threading. All in good time.

So here's my uncommented and fully unnecessary data type usage.

Behold:

{{< highlight c >}}
#include <stdio.h>
#include <math.h>
#include <stdlib.h>

unsigned long int gcd(unsigned long int e, unsigned long int f);
unsigned long int tot(unsigned long int t);

int main(int argc, char *argv[])
{
    if (argc < 3 || argc > 3) { printf("Usage: %s first second\n",
argv[0]); exit(0); }

    unsigned long int a = strtol(argv[1], NULL, 10);
    unsigned long int b = strtol(argv[2], NULL, 10);
    unsigned long int i;

    if (a > b) { printf("First must be lower than second.\n"); }

    for ( i = a ; i <= b ; i++ )
    {
        printf("%d, %d\n", i, tot(i));
    }

    exit(0);
}

unsigned long int gcd(unsigned long int a, unsigned long int b)
{
    unsigned long int c;
    while ( a != 0 ) 
    {
        c = a;
        a = b % a;
        b = c;
    }
    return b;
}

unsigned long int tot(unsigned long int t)
{
    unsigned long int y = 0;
    unsigned long int o = t;
    while ( t != 0 ) 
    {
        if (gcd(o, t) == 1) 
        {
            y++;
        }
        t--;
    }
    return y;
}
{{< / highlight >}}
