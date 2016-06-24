---
title: C++ articles
layout: post
tags: [cpp]
---

This is a list of resources for learning a little less known topics in C++:

1. **[Comma Operator](https://en.wikipedia.org/wiki/Comma_operator)** :

    Understand the difference between the instance of `,` as an operator (as in `return cout << "Hello", 0;`)
    and as a separator (as in `func(1, 2)`).

    Things you should know:

    1. `,` operator has lowest precedence of all C/C++ operators, and is left associative.
    2. `,` operator maybe overloaded by a library. [ref](http://stackoverflow.com/a/54172/3821813)

    **Further References:** [SO \| How does the comma operator work](http://stackoverflow.com/questions/54142/how-does-the-comma-operator-work), [SO \| Proper use of comma operator](http://stackoverflow.com/questions/17902992/what-is-the-proper-use-of-the-comma-operator)

    ---

2. **[Undefined Behaviour and Sequence Points](http://stackoverflow.com/questions/4176328/undefined-behavior-and-sequence-points)**

    Understand common sources of UB and gain knowledge of Sequence Points and their relation with UB.

    Things you should know:

    1. UB means anything can happen, from daemons flying out of your nose to your girlfriend getting pregnant.
    2. Why would this lead to UB, `printf("%d %d", i, ++i);`

    **Further References:** [SO \| Common Undefined Behaviours in C++](http://stackoverflow.com/questions/367633/what-are-all-the-common-undefined-behaviours-that-a-c-programmer-should-know-a?rq=1)

    ---

3. **[rValues and lValues](http://thbecker.net/articles/rvalue_references/section_01.html)**

    Understand the difference between lValues and rValues.

    ---

4. **[Strict Weak Ordering](http://www.sgi.com/tech/stl/StrictWeakOrdering.html)**

    Understand what is strict weak ordering. Note that `std::sort` requires a sorter which satisfies
    the strict weak ordering rule. As an example, the following definition of `<operator` *may* cause
    `std::sort` to crash, since this is neither *irreflexive*, nor *anti symmetric*

        struct data {
            int x;
            bool operator<(const data &other) const {
                return x <= other.x;
            }
        };

    ---
