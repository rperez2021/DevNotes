---
id: nppylaujf1ml0o7zcp8gu34
title: Webpack
desc: 'Notes on Webpack'
updated: 1648687756744
created: 1648687756744
---
## General Info

At its core, **webpack** is a static module bundler for modern JavaScript applications. When webpack processes your application, it internally builds a dependency graph from one or more entry points and then combines every module your project needs into one or more bundles, which are static assets to serve your content from.

## Tips

- If a `webpack.config.js` is present, the webpack command picks it up by default. We use the --config option only to show that you can pass a configuration of any name. This will be useful for more complex configurations that need to be split into multiple files.
- Custom parameters can be passed to webpack by adding two dashes between the `npm run build` command and your parameters, e.g. `npm run build -- --color`.
- It is important to remember that when defining rules in your webpack config, you are defining them under `module.rules` and not `rules`. For your benefit, webpack will warn you if this is done incorrectly.
- Keep in mind that when using regex to match files, you may not quote it. i.e `/\.txt$/` is not the same as `'/\.txt$/'` or `"/\.txt$/"`. The former instructs webpack to match any file that ends with .txt and the latter instructs webpack to match a single file with an absolute path `'.txt'`; this is likely not your intention.
