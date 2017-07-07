---
layout: post
title: Continuously Build
---

I can't overstate the peace of mind that working on a project with comprehensive tests give me.  It truly amazes me how much better code I produce with I feel confident that the changes I'm making aren't breaking things.

To have that confidence, I need to run my tests.

When my tests run as part of my regular workflow, my confidence is high and the code I produce is better.

You may be like me: if you are, I'd like you to feel that confidence as well.

You also might be lazy.  Lucky for the both of us, there are several ways of automatically running tests, so we can be lazy and smug.

## workflow

save > the tests run > you get notified

If it's more complicated than that, you might just not run those tests.

## tools

### fswatch

We don't need advanced tooling to automate test runs.

[fswatch](https://github.com/emcrisostomo/fswatch/wiki/How-to-Use-fswatch) can be used do watch the filesystem for changes and run commands.  For OSX, it can easily be installed with `brew install fswatch`.

To watch an entire directory, use

`fswatch -o . | xargs -n1 -I{} [YOUR_BUILD_COMMAND_HERE]`

When working on [Exercism.io](http://exercism.io/) exercises, I simply invoke the command line test execution on any change to the current directory:

`fswatch -o . | xargs -n1 -I{} groovy HelloWorldSpec.groovy`

### Guard

My first experience getting continuous feedback was with [Guard for Ruby projects](https://github.com/guard/guard).

Follow the [Guard installation instructions for your project](https://github.com/guard/guard), run

```
bundle exec guard
```

in a shell, and be happy.

### Eclipse / IntelliJ Idea

If you happen to be working in either of these IDEs, go get [Infinitest](https://infinitest.github.io/).

When using Spock or JUnit testing frameworks, I've found that Inifitest will automatically find my tests and execute them whenever one of the test dependencies changes.  A small bar in the lower-left hand corner of my Eclipse window shows me the test run status.

![_config.yml]({{ site.baseurl }}/images/infinitest-eclipse-status.png)

### Gradle

If the project you're working on has a lingua franca build tool, use it.  If it doesn't, use Gradle.

Gradle is a build system.  Examples of what kinds of languages supported are Java, Groovy, Scala, Kotlin, Antlr, assembler, C, C++, Objective C, JEE, Ruby, NodeJS, Sass, SCSS.  Typing examples of compilation frameworks that are supported would hurt my hands.

Continuously build Gradle projects with

`./gradlew <target> --continuous`

* `./gradlew check --continuous`
* `./gradlew test --continuous`

Put this in `~/.gradle/init.d/` to get build announcements for all your projects, without needing to add the plugin to an individual project.

{% gist Dispader/a74a5daa10f7e128bed57b13c0cb1fa2 %}

## notifications

I currently develop in OSX most of the time.  If that's true for you, you'll want to know something about the state of notifications for OSX.

OSX previously shipped without a notification system.

A great system, [Growl](http://growl.info/), was developed for notifications.  Growl was open source and freely available.  As a result, many notification tools developed using the [Growl API](http://growl.info/documentation/developer/).

The Growl folks decided to close the source of their project, and [offer it up on the App Store](https://itunes.apple.com/us/app/growl/id467939042?mt=12) at a modest price.

Unfortunately for tools that used the Growl API (like the Gradle plugin above), the now-dependent software can't include Growl in the distribution.

Fortunately for us [this post describes how to use a version of Growl, which was forked from a point in time when it was an Open Source project](http://www.nbcdaily.com/the-easy-free-way-to-send-growl-messages-to-your-macs-notification-center/28091/).

This works well for me, but only if I also install the `growlnotify` add-on, which is included in the downloaded package.﻿

## references

* [how to](https://gist.github.com/Dispader/a74a5daa10f7e128bed57b13c0cb1fa2#file-build-announcements-gradle) add [`build-announcements`](https://docs.gradle.org/current/userguide/build_announcements_plugin.html) to your local Gradle installation
* [The Easy, Free Way To Send Growl Messages To Your Mac’s Notification Center](http://www.nbcdaily.com/the-easy-free-way-to-send-growl-messages-to-your-macs-notification-center/28091/)
* [Infinitest](https://infinitest.github.io/)
* [`fswatch`](https://github.com/emcrisostomo/fswatch)
* [`guard`](https://github.com/guard/guard)
