---
title: 'Prefix Naming and Compatibility'
date: 2025-07-30
---

The annual summer of re-development continues as people rush to fix iOS beta bugs and adopt new APIs while they still have existing users to support. Standing with one foot in each camp means cutting against the grain of Apple’s “we only look forward” philosophy. Recent discussion online reminded me of a useful trick old enough it risks being forgotten.

Let’s start with the problem: you want to adopt a new feature like .glassEffect() for iOS 26. But older versions don’t know what glass effect is so instead of:

    Button(“Buy Now”).glassEffect()

You write:

    if #available(iOS 26.0, *) {
        Button(“Buy Now”).glassEffect()
    } else {
        Button(“Buy Now”)
    }

By default, you get to repeat this every place you need to access a new feature or work around a platform deficiency. Your codebase becomes littered with Apple’s design decisions. You hear internet rants and podcast discussions about how UI rework consumes months that could go toward new features rather than lipstick.

We can borrow from Apple’s earlier documentation and a time in history when the platform vendor treated third parties as potential allies rather than uninvited guests. Paraphrasing [Apple’s own documentation](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/Conventions/Conventions.html) from the Objective-C era: “You should avoid using generic names like View or glassEffect. In order to keep names unique, the convention is to use prefixes [...] Your own classes should use three letter prefixes.” Apple no longer follows this rule, but we can still leverage it:

    extension View {
        @ViewBuilder func tmlGlassEffect() -> some View {
            if #available(iOS 26, *) {
                self.glassEffect()
            } else {
                self 
            }
        }
    }

    Button(“Buy Now”).tmlGlassEffect()

This is a little bit more code, and I would not wrap every single class, component or function you customize. But, the inherent grep-ability of the unique name gives you an instantly auditable list of what’s using it. This is the upside Apple was trying to offer developers; the idea of a “namespace clash” dates back to Smalltalk and contemporary Objective-C code rarely suffered from it. When Swift added modules, prefixing was treated as an anachronism, and the official guidance threw the baby out with the bathwater.

This principle scales beyond simple compatibility shims. In my day to day work with a portfolio of apps, we end up using two prefixes in an app. One prefix marks custom code for the app and another marks custom code reused between apps. This encourages the right amount of copy and paste. Once functionality has proven its value, it’s promoted up to the shared namespace. After its promotion, example use cases are easy to find via search.

Naming things isn’t hard in the sense of requiring genius or force of will, it’s hard in the sense of asking for a disciplined, thoughtful approach. Prefixes aren’t just about avoiding conflicts - they enable discovery. The small upfront cost in planning pays dividends every time you need to understand or evolve your codebase. I hope this helps in your endeavors!