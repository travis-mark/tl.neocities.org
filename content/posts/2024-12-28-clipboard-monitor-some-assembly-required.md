---
title: 'Clipboard Monitor: Some Assembly Required'
date: 2024-12-28
tags: tech
---

## Some Assembly Required, Batteries Never Included

My wife, my best friend and I are in a group chat where we post daily puzzle scores. Occasionally, I'll put together a graph or logger. Because it's a fairly bounded exercise, I use it to evaluate programming languages, frameworks or approaches. This time, I'm taking the pulse on current LLMs' ability to solve the problem, rather than the solution itself.

### The Wordle Monitor

The random thought I had this morning was to build a "zero effort" version. Instead of creating some spreadsheet or form to paste scores into, I wanted detect the scores as they enter my clipboard. The automated nature limits its use to my scores only, which is fine as an exercise.

    Wordle 1,288 3/6*

    🟨⬛🟨🟨⬛
    🟩🟩🟩⬛⬛
    🟩🟩🟩🟩🟩

is copied, but this is written to a file:

    <timestamp>|Wordle|1,288|3|*

### Speak to My Serpent

Ideally, you grab some existing automation program and configure it with a regex. In my case, I already have one a [previous exercise](/tools/score-parser/) (translated to Python regex):

    /(Wordle) ([0-9,]+)[ 🎉]* (\w)\/6(?[*]?)\n([⬛🟨⬜🟩\n]+)/

Unfortunately, the internet had other plans. I sent a query to four LLMs ([ChatGPT](https://chatgpt.com), [Claude](https://claude.ai/chat/), [Gemini](https://gemini.google.com/), [Meta](https://www.meta.ai/)) and two search engines ([Google](https://www.google.com/) and [Brave](https://search.brave.com/)) expecting them to suggest an such a tool. Search and AI quality is a moving target, but what I found matched my expectations.

Given the input:

    On my mac, when something is copied to a clipboard, I want to check it against a regular expression and perform some action if a match is found. What is a good way to do this?

- ChatGPT and Claude suggested a working Python script.
- Gemini and Meta suggested non-working scripts, Python and Applescript respectively.
- Google and Brave offered up solutions or apps like ClipMenu most of which would not fulfill the need.

It's sad how bad search has gotten. There **are** friendlier answers to this problem, but running python isn't that hard, right?

### Do You Even Python?

[Python](https://www.python.org/) is one of the most popular programming languages. It's pre-installed on Linux and installable on Windows. Macs used to also have it pre-installed, until a circa 2019 decision to mark the version Apple uses for its own tools private and unavailable to customers. More on that later.

The install steps required aren't particularly arduous, but any guidance I offer isn't likely to age well. This is why basic scripting tools should ship pre-installed! You'll have to do your own homework here.

### Solving the Actual Problem

After a few rounds of tweaks, I got something up and running. You can view it in its clearly hacked together glory, [here](https://github.com/travis-mark/dotfiles/blob/master/bin/clipboard-monitor.py). I added it to launchctl to run at startup and remain available in the background.

### What is a Computer, Really?

This example runs on my laptop. It could run on yours. During my research into a mobile version, I receieved this very predictable response:

    Apps cannot monitor the clipboard continuously in the background due to security/privacy restrictions.

I guess everyone who does Wordle on a phone is left out in the cold. 