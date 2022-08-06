## General Info

At its core, **webpack** is a static module bundler for modern JavaScript applications. When webpack processes your application, it internally builds a dependency graph from one or more entry points and then combines every module your project needs into one or more bundles, which are static assets to serve your content from.

## Tips

- If a `webpack.config.js` is present, the webpack command picks it up by default. We use the --config option only to show that you can pass a configuration of any name. This will be useful for more complex configurations that need to be split into multiple files.
- Custom parameters can be passed to webpack by adding two dashes between the `npm run build` command and your parameters, e.g. `npm run build -- --color`.
- It is important to remember that when defining rules in your webpack config, you are defining them under `module.rules` and not `rules`. For your benefit, webpack will warn you if this is done incorrectly.
- Keep in mind that when using regex to match files, you may not quote it. i.e `/\.txt$/` is not the same as `'/\.txt$/'` or `"/\.txt$/"`. The former instructs webpack to match any file that ends with .txt and the latter instructs webpack to match a single file with an absolute path `'.txt'`; this is likely not your intention.
- Webpack uses a regular expression to determine which files it should look for and serve to a specific loader. In this case, any file that ends with .css will be served to the style-loader and the css-loader.

## Module Loading

Module loaders can be chained. Each loader in the chain applies transformations to the processed resource. A chain is executed in reverse order. The first loader passes its result (resource with applied transformations) to the next one, and so forth. Finally, webpack expects JavaScript to be returned by the last loader in the chain.

```javascript
module: {
    rules: [
      {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
```

## Output Management

As your application grows and once you start using hashes in filenames and outputting multiple bundles, it will be difficult to keep managing your index.html file manually. However, a few plugins exist that will make this process much easier to manage.

[HtmlWebpackPlugin](https://github.com/jantimon/html-webpack-plugin)

### The Manifest

You might be wondering how webpack and its plugins seem to "know" what files are being generated. The answer is in the manifest that webpack keeps to track how all the modules map to the output bundles. If you're interested in managing webpack's output in other ways, the manifest would be a good place to start.

The manifest data can be extracted into a json file for consumption using the [WebpackManifestPlugin](https://github.com/shellscape/webpack-manifest-plugin).

## Development Environement

### Source Maps

When webpack bundles your source code, it can become difficult to track down errors and warnings to their original location. For example, if you bundle three source files (a.js, b.js, and c.js) into one bundle (bundle.js) and one of the source files contains an error, the stack trace will point to bundle.js. This isn't always helpful as you probably want to know exactly which source file the error came from.

In order to make it easier to track down errors and warnings, JavaScript offers source maps, which map your compiled code back to your original source code. If an error originates from b.js, the source map will tell you exactly that.

As the name suggests, a source map consists of a whole bunch of information that can be used to map the code within a compressed file back to it’s original source. You can specify a different source map for each of your compressed files.

You indicate to the browser that a source map is available by adding a special comment to the bottom of your optimised file.

`//# sourceMappingURL=/path/to/script.js.map`

This comment will usually be added by the program that was used to generate the source map. The developer tools will only load this file if support for source maps is enabled and the developer tools are open.

You can also specify a source map is available by sending the `X-SourceMap` HTTP header in the response for the compressed JavaScript file.

`X-SourceMap: /path/to/script.js.map`

The source map file contains a JSON object with information about the map itself and the original JavaScript files. Here is a simple example:

```json
{
    version: 3,
    file: "script.js.map",
    sources: [
        "app.js",
        "content.js",
        "widget.js"
    ],
    sourceRoot: "/",
    names: ["slideUp", "slideDown", "save"],
    mappings: "AAA0B,kBAAhBA,QAAOC,SACjBD,OAAOC,OAAO..."
}
```

- `version` – This property indicates which version of the source map spec the file adheres to.
- `file` – The name of the source map file.
- `sources` – An array of URLs for the original source files.
- `sourceRoot` – (optional) The URL which all of the files in the sources array will be resolved from.
- `names` – An array containing all of the variable and function names from your source files.
- `mappings` – A string of Base64 VLQs containing the actual code mappings. (This is where the magic happens.)

Using source maps allows developers to maintain a straight-forward debugging environment while at the same time optimizing their sites for performance.

## Hot Module Replacement

Hot Module Replacement (or HMR) is one of the most useful features offered by webpack. It allows all kinds of modules to be updated at runtime without the need for a full refresh. This page focuses on implementation while the concepts page gives more details on how it works and why it's useful.
