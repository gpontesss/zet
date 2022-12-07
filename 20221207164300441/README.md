---
id: 20221207164300441
tags: ["C", "size_t", "uint", "int"]
---

# How binary signed integers work

A binary unsigned integer stores the same value as the regular number does,
i.e., 0b1111 really stores 7, considering a memory system that words up to 4
bits in each address.[^1] That is true for every unsigned integer value.  This
changes with signed integers.  One of the bits has to store data related to its
sign. That's the left-most bit. 1 signs a negative number; a 0, a positive
number. This property is interesting for it makes positive signed integers
directly convertible to unsigned integers: 0b0111 is 7 when stored both as uint
and int. It also implies that negative numbers will represent different values
depending of what data type it is interpreted as, i.e., 0b1111 is 15 as an
unsigned integer, but -1 as a a signed integer.

Why 0b1111 as a signed integer means -1 instead of -7? Binary negatives are
represented by their complement incremented by 1. So -1 will be the complement
of 0b0001 --- 0b1110 --- summed with 1: 0b1110 + 0b0001 = 0b1111. Following
this rule, -7 is 0b1000 + 0b0001, which is 0b1001. This property is
interesting, for -8 (0b1000) should be the lowest value possible to
represent[^2] and, if further decremented, should "wrap around" and turn into
the highest possible number --- 7 ---, which is indeed what happens: -1 =
0b1111; -8 = 0b1000; 0b1111 + 0b1000 = 0b0111.

[^1]: This is is assumed for further examples.
[^2]: Considering a words up to 4 bits, the number of possible numbers is 16
    (2^4). Thus, there are 8 combinations that start with 0 (1 * 2 * 2 * 2),
    and 8 that start with 1. The highest possible value is 7, for 0b0111 is the
    highest possible number ending with 0, and having zero counted as a positive,
    as its left-most digit is a 0; the lowest value is -8.
