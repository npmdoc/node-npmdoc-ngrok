# npmdoc-ngrok

#### basic api documentation for  [ngrok (v2.2.6)](https://github.com/bubenshchykov/ngrok#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-ngrok.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-ngrok) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-ngrok.svg)](https://travis-ci.org/npmdoc/node-npmdoc-ngrok)

#### node wrapper for ngrok

[![NPM](https://nodei.co/npm/ngrok.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/ngrok)

- [https://npmdoc.github.io/node-npmdoc-ngrok/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-ngrok/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-ngrok/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-ngrok/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-ngrok/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-ngrok/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "bubenshchykov"
    },
    "bin": {
        "ngrok": "./bin/ngrok"
    },
    "bugs": {
        "url": "https://github.com/bubenshchykov/ngrok/issues"
    },
    "dependencies": {
        "async": "^0.9.0",
        "decompress-zip": "^0.3.0",
        "lock": "^0.1.2",
        "request": "^2.55.0",
        "uuid": "^3.0.0"
    },
    "description": "node wrapper for ngrok",
    "devDependencies": {
        "chai": "~1.8.1",
        "homedir": "^0.6.0",
        "mocha": "~1.14.0"
    },
    "directories": {},
    "dist": {
        "shasum": "404cb8ef7e11dcd399e17b3c76c5dc56aa79849a",
        "tarball": "https://registry.npmjs.org/ngrok/-/ngrok-2.2.6.tgz"
    },
    "files": [
        "index.js",
        "postinstall.js",
        "bin/ngrok"
    ],
    "gitHead": "607bdcbbda05d290e5095510392ff89d09706cae",
    "homepage": "https://github.com/bubenshchykov/ngrok#readme",
    "keywords": [
        "ngrok",
        "localhost",
        "tunneling",
        "localtunnel",
        "webhook"
    ],
    "license": "BSD-2-Clause",
    "main": "index.js",
    "maintainers": [
        {
            "name": "bubenshchykov"
        }
    ],
    "name": "ngrok",
    "optionalDependencies": {},
    "repository": {
        "type": "git",
        "url": "git://github.com/bubenshchykov/ngrok.git"
    },
    "scripts": {
        "postinstall": "node ./postinstall.js",
        "postupdate": "node ./postinstall.js",
        "test": "node ./node_modules/mocha/bin/_mocha"
    },
    "version": "2.2.6"
}
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
