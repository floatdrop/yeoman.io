---
layout: post
title: Composability. Where are we
category: blog
---

## Composability. Where are we

You may have followed some of the `[Composability]` talks we recently had on the [yeoman/generator issue tracker](https://github.com/yeoman/generator).

In this post we want to review what we currently have, what we're currently working on and what we'll need to do in the future.

### What is "composability" in the Yeoman context?

Composability is:

- The capacity for a generator author to build its generator on top of another one. (e.g. Compose Generator-Angular on Generator-Karma)
- The capacity for the end user to build custom application choosing relevant generators for it's use case. (e.g. I want to use Yeoman to scaffold an Emberjs application on top of a Laravel server and using Sass for CSS)

These two types of composability needs are differents and need specifics API.

### The current state

#### Hooking

Currently, the Base generator have a built-in hook system that allow a generator from running another time at run time. You'd hook a generator like this:

``` javascript
this.hookFor('karma', { as: 'app' });

// But it would be cleaner this way
this.hookFor('test-util', { default: 'karma' });
```

Doing so, you also generate an option (`--test-util`) allowing user to override the default test utility.

```
$ yo gen --test-util=mocha
```

Hooks are OK and allow easy abstraction of third party generators. Although, they're not perfect. Hooks are run synchronously which make for a weird workflow; you generator ask question, generates files, launch NPM/Bower, then the hooked generator start and do the same. Also, exporting an option, it makes it for less reliable behavior as the hooked generator may not be compatible.