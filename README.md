# node-jose-browserify #

Emulates Cisco's node-jose module for the browser.

PR https://github.com/cisco/node-jose/pull/264 is raised to merge the changes with the node-jose repo

Refer to https://github.com/cisco/node-jose for documentation.

## Angular Usage ##

Import and use as any other package. All the methods will be supported in the browser, just as in node.js.

```javascript
import * as jose from 'node-jose';
```

The following changes are required to make few node-modules available in the browser

- angular compilerOptions for stream

    In `tsconfig.json` , *compilerOptions* add
    ```json
    "paths": {
        "stream": ["../node_modules/stream-browserify/index.js"]
    }
    ```
    This is to avoid the below error
    > ERROR in ./node_modules/browserify-zlib/lib/index.js.
    > Module not found: Error: Can't resolve 'stream' in '***/node_modules/browserify-zlib/lib'
- polyfil for global object
    In `polyfills.ts` add 
    ```
    // Polyfill for node-jose
    (window as any)['global'] = window;
    ```
    This is to avoid the below error
    > Uncaught ReferenceError: global is not defined


### Merging node-jose updates

To pull the latest updates from node-jose into node-jose-browserify
```
$ git pull https://github.com/cisco/node-jose.git master
```