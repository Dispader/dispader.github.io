---
layout: post
title: Grab Dependencies in the Groovy Shell
---

## groovysh

I'm a command line person, and I love the interactive nature of Ruby's `irb` for extemporaneous coding.  Groovy comes with its own analogue, the [Groovy Shell](http://groovy-lang.org/groovysh.html) (`groovysh`, which the parallelist in me would like to see renamed to `igr`).

But JVM ecosystem has rich tools for pulling in and managing dependencies (and transient dependencies).  Generally, you can specify new [Ivy/Maven/etc.](http://mvnrepository.com/) dependencies in the build, or (in Groovy) as `@Grab` annotations.  But trying things out interactively is something that was a bit cumbersome.  It could be done, with metaprogramming or making things available to the classpath before executing `groovysh`, or making an ugly call into the Grab functions inside Groovy.

But that is work.  And I am lazy.

Also, these methods wouldn't allow for auto-completion of imports, so you'd have to type.  And I just told you how I feel about working.

## grab and smash

I've written a [small command for the Groovy Shell](https://github.com/Dispader/groovysh-command-grab) that allows grabbing dependencies, installing them in the runtime environment, and allowing for import auto-completion.

`:load` it from your Groovy Shell by [URL](https://git.io/v2N1I), and enjoy!

{% gist Dispader/8697fbafc71daa7a2575 %}

## *update*

[Pull request #286](https://github.com/apache/groovy/pull/286) has been merged, so you we should be able to expect the above feature in the standard Groovy core version of `groovysh`.
