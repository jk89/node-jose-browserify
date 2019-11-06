[![published](https://static.production.devnetcloud.com/codeexchange/assets/images/devnet-published.svg)](https://developer.cisco.com/codeexchange/github/repo/NewtonJoshua/node-jose-browserify)
![download total](https://img.shields.io/npm/dt/node-jose-browserify.svg)

# node-jose-browserify #

An advanced version of Cisco's node-jose module that works in both browser and the server. It is compatible with node.js and angular

Refer to https://github.com/cisco/node-jose for documentation.


### PR ###

The PR [Angular Support: To make node-jose work in angular apps](https://github.com/cisco/node-jose/pull/264) is raised to merge the changes with the node-jose repo.

Since the node-jose repo is not actively maintained now, this PR can't be merged. So this fork is published.

Dependencies Added:
- browserify-zlib: In the browser if Node's 'zlib' can't be resolved, browserify-zlib can be used.
- buffer: make buffer, that emulates node's Buffer API, available globally in the browser
- process: make process, that emulates node's Process API, available globally in the browser
- stream-browserify: this should be used by zlib/browserify-zlib instead of 'stream'. Should be mentioned in angular compiler options.

The steps to use node-jose in angular app is added in the readme file.

### Install ###

```javascript
    npm i node-jose-browserify
```


## Angular Usage ##

Import and use as any other package. All the methods will be supported in the browser, just as in node.js.

```javascript
import * as jose from 'node-jose-browserify';
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
