# rollup-plugin-inject

Scan modules for global variables and inject `import` statements where necessary


## Installation

```bash
npm install --save-dev rollup-plugin-inject
```


## Usage

```js
import { rollup } from 'rollup';
import inject from 'rollup-plugin-inject';

rollup({
  entry: 'main.js',
  plugins: [
    inject({
      // control which files this plugin applies to
      // with include/exclude
      exclude: 'node_modules/**',

      // all other options are treated as modules...

      // use the default – i.e. insert
      // import $ from 'jquery'
      $: 'jquery',

      // use a named export – i.e. insert
      // import { Promise } from 'es6-promise'
      Promise: [ 'es6-promise', 'Promise' ],

      // use a local module instead of a third-party one
      'Object.assign': path.resolve( 'src/helpers/object-assign.js' ),

      // ...but if you want to be careful about separating modules
      // from other options, supply `options.modules` instead
      modules: {
        $: 'jquery',
        Promise: [ 'es6-promise', 'Promise' ],
        'Object.assign': path.resolve( 'src/helpers/object-assign.js' )
      }
    })
  ]
}).then(...)
```
