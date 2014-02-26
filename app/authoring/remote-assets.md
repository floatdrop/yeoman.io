---
layout: default
---

# Fetching remote assets

Your generator may need to fetch remote packages or assets (e.g.: Wordpress, Rails, a boilerplate project, etc).

Usually the best way is to use a package manager to handle the dependencies for you. This reduce overhead and the downloading time. If your case cannot be resolved using a package manager, Yeoman provides some methods to dynamically requests assets from remote URLs.

## Using NPM

We'll cover how to fetch remote assets with npm, but the same concept will apply to any other tools.

Instead of version number, your `package.json` can contains raw URLs to fetch. These can point to standalone resources or to git repositories.

```json
{
  "dependenncies": {
    "html5-boilerplate": "h5bp/html5-boilerplate", // fetch https://github.com/h5bp/html5-boilerplate.git
    "html5-boilerplate": "h5bp/html5-boilerplate#59c10b", // fetch a precise version
    
  }
}
```

## Fetch mixins

When fetching built release from a project (usually `.zip` or `.tar` files), the npm way may fall short. It's to cover these cases the Yeoman fetch mixin have been added to core.

Make sure to checkout the full [API documentation](http://yeoman.github.io/generator/fetch.html) for a list of all resources.

### `generator.fetch(file, destination, cb)`

Fetch a remote URL resource.

- `file` the URL to fetch
- `destination` the file where to write the source
- `cb` a callback once it is done.

### `generator.extract()`

Extract present the same API as `generator.fetch()`. The only difference is that `extract` will actually extract archive formats to the specified location folder.
