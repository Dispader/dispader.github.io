---
layout: post
title: Preventing JVM Apps from Losing focus in OSX
---

## statement of sadness

A while ago I switched from Linux-nearly-everywhere to a MacBook Pro for my main iron.

I run JVM applications.  A lot of JVM applications.  Most were well-behaved, but some of them lost focus on launch.

1. be in a terminal shell (aren't we folks always?)
1. type `groovysh`
1. expected:
    1. continue typing to the terminal, interacting happily with the Groovy shell
1. actual:
    1. terminal loses focus
    1. `alt-tab` shows an application called `GroovyShell`, with a circular G icon
    1. that application shows as an Xcode development item
    1. forget that focus was lost, type, be sad

![_config.yml]({{ site.baseurl }}/images/groovy-shell.png)

## make the pain go

If you want the pain to stop, add a JVM environment flag somewhere in your environment startup sequence.  I prefer to do such things in my `~/.bashrc`.

{% gist Dispader/39ffcb8cc783c7a47d4a %}

(The T.S. Eliot quote is optional.  It's possible you don't want to think about T.S. Eliot poetry when you edit your dotfiles and smile.  Your life is your own.)

## ?

Bref, JVM processes that need some kinds of resources (to optimize the resizing of images, etc.) invoke another kind of process, one that ususally uses elements related to display.  These can register as using the display.  OSX responds in a way that is not very helpful.
