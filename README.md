## Split By Path Webpack Plugin

This plugin will split your entry bundle into any number of arbitrarily defined smaller bundles.

## Credits

This plugin is based on [split-by-name-webpack-plugin](https://github.com/soundcloud/split-by-name-webpack-plugin).

### How?

Configuration of the plugin is simple. You instantiate the plugin with a single option: `buckets` which should be an
array of objects, each containing the keys `name` and `regex`. Any modules which are in your entry chunk which match the
bucket's regex (first matching bucket is used), are then moved to a new chunk with the given name.

Creating a 'catch-all' bucket is not necessary: anything which doesn't match one of the defined buckets will be left in
the original chunk.

### Example

```js
var SplitByPathPlugin = require('split-by-path-webpack-plugin');
module.exports = {
  entry: {
    app: 'app.js'
  },
  output: {
    path: __dirname + '/dist',
    filename: "[name]-[chunkhash].js",
    chunkFilename: "[name]-[chunkhash].js"
  },
  plugins: [
    new SplitByPathPlugin({
      buckets: [{
        name: 'vendor',
        regex: /(node_modules\/|src\/vendor\/)/
      }]
    })
  ]
};
```
