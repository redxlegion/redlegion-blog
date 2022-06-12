---
comments: true
date: "2016-02-27T12:45:00Z"
music: Total Silence
categories:
- info
tags:
- c
- chamfer
- calculator
title: Chamfer Calculator in C
---

I've converted the [Rust Chamfer Calculator]({{< ref
2015-08-09-Chamfer-calculator-in-rust >}}) to C for shits and giggles,
and to learn something new. If you have any recommendations on
tutorials for C socket programming, please feel free to contact me.
Without further ado, here's my garbage:

{{< highlight c >}}
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

double to_radians(double degrees);
double chamf(double angle, double depth, double bore);

int main(int argc, char *argv[])
{
        if (argc < 4 || argc > 4)
        {
                printf("Usage: %s angle depth bore\n", argv[0]);
                exit(0);
        }

        double ang = strtod(argv[1], NULL);
        double dep = strtod(argv[2], NULL);
        double bor = strtod(argv[3], NULL);

        double cha = chamf(ang, dep, bor);

        printf("Angle: %f\nDepth: %f\nBore: %f\nChamfer Diameter:
%.16f\n", ang, dep, bor, cha);

        exit(0);
}

double to_radians(double degrees)
{
        return degrees * (M_PI / 180);
}

double chamf(double angle, double depth, double bore)
{
        return (tan(to_radians(angle)) * depth) + bore;
}
{{< / highlight >}}
