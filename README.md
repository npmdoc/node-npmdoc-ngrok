# api documentation for  [ngrok (v2.2.6)](https://github.com/bubenshchykov/ngrok#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-ngrok.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-ngrok) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-ngrok.svg)](https://travis-ci.org/npmdoc/node-npmdoc-ngrok)
#### node wrapper for ngrok

[![NPM](https://nodei.co/npm/ngrok.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/ngrok)

[![apidoc](https://npmdoc.github.io/node-npmdoc-ngrok/build/screenCapture.buildCi.browser.apidoc.html.png)](https://npmdoc.github.io/node-npmdoc-ngrok/build/apidoc.html)

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



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module ngrok](#apidoc.module.ngrok)
1.  [function <span class="apidocSignatureSpan">ngrok.</span>authtoken (token, cb)](#apidoc.element.ngrok.authtoken)
1.  [function <span class="apidocSignatureSpan">ngrok.</span>connect (opts, cb)](#apidoc.element.ngrok.connect)
1.  [function <span class="apidocSignatureSpan">ngrok.</span>disconnect (publicUrl, cb)](#apidoc.element.ngrok.disconnect)
1.  [function <span class="apidocSignatureSpan">ngrok.</span>kill (cb)](#apidoc.element.ngrok.kill)
1.  number <span class="apidocSignatureSpan">ngrok.</span>_eventsCount
1.  object <span class="apidocSignatureSpan">ngrok.</span>_events
1.  object <span class="apidocSignatureSpan">ngrok.</span>domain

#### [module ngrok._events](#apidoc.module.ngrok._events)
1.  [function <span class="apidocSignatureSpan">ngrok._events.</span>error ()](#apidoc.element.ngrok._events.error)



# <a name="apidoc.module.ngrok"></a>[module ngrok](#apidoc.module.ngrok)

#### <a name="apidoc.element.ngrok.authtoken"></a>[function <span class="apidocSignatureSpan">ngrok.</span>authtoken (token, cb)](#apidoc.element.ngrok.authtoken)
- description and source-code
```javascript
function authtoken(token, cb) {
	cb = cb || noop;
	var a = spawn(
		bin,
		['authtoken', token],
		{cwd: __dirname + '/bin'});
	a.stdout.once('data', done.bind(null, null, token));
	a.stderr.once('data', done.bind(null, new Error('cant set authtoken')));

	function done(err, token) {
		cb(err, token);
		a.kill();
	}
}
```
- example usage
```shell
...
ngrok http 8080
'''

## authtoken
You can create basic http-https-tcp tunnel without authtoken. For custom subdomains and more you should  obtain authtoken by signing
 up at [ngrok.com](https://ngrok.com). Once you set it, it's stored in ngrok config and used for all tunnels. Few ways:

'''
ngrok.authtoken(token, function(err, token) {});
ngrok.connect({authtoken: token, ...}, function (err, url) {});
ngrok authtoken <token>
'''

## connect
'''javascript
var ngrok = require('ngrok');
...
```

#### <a name="apidoc.element.ngrok.connect"></a>[function <span class="apidocSignatureSpan">ngrok.</span>connect (opts, cb)](#apidoc.element.ngrok.connect)
- description and source-code
```javascript
function connect(opts, cb) {

	if (typeof opts === 'function') {
		cb = opts;
	}

	cb = cb || noop;
	opts = defaults(opts);

	if (api) {
		return runTunnel(opts, cb);
	}

	lock('ngrok', function(release) {
		function run(err) {
			if (err) {
				emitter.emit('error', err);
				return cb(err);
			}
			runNgrok(opts, release(function(err) {
				if (err) {
					emitter.emit('error', err);
					return cb(err);
				}
				runTunnel(opts, cb)
			}));
		}

		opts.authtoken ?
			authtoken(opts.authtoken, run) :
			run(null);
	});
}
```
- example usage
```shell
...
usage
===

[![NPM](https://nodei.co/npm/ngrok.png?global=true&&downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/ngrok/)

'''
var ngrok = require('ngrok');
ngrok.connect(function (err, url) {});

or

npm install ngrok -g
ngrok http 8080
'''
...
```

#### <a name="apidoc.element.ngrok.disconnect"></a>[function <span class="apidocSignatureSpan">ngrok.</span>disconnect (publicUrl, cb)](#apidoc.element.ngrok.disconnect)
- description and source-code
```javascript
function disconnect(publicUrl, cb) {
	cb = cb || noop;
	if (typeof publicUrl === 'function') {
		cb = publicUrl;
		publicUrl = null;
	}
	if (!api) {
		return cb();
	}
	if (publicUrl) {
		return api.del(
			tunnels[publicUrl],
			function(err, resp, body) {
				if (err || resp.statusCode !== 204) {
					return cb(err || new Error(body));
				}
				delete tunnels[publicUrl];
				emitter.emit('disconnect', publicUrl);
				return cb();
			});
	}

	return async.each(
		Object.keys(tunnels),
		disconnect,
		function(err) {
			if (err) {
				emitter.emit('error', err);
				return cb(err);
			}
			emitter.emit('disconnect');
			return cb();
		});
}
```
- example usage
```shell
...
Other options: 'name, inspect, host_header, bind_tls, hostname, crt, key, client_cas, remote_addr' - read [here](https://ngrok.com
/docs)

Note on regions: region used in first tunnel will be used for all next tunnels too.

## disconnect
The ngrok and all tunnels will be killed when node process is done. To stop the tunnels use
'''javascript
ngrok.disconnect(url); // stops one
ngrok.disconnect(); // stops all
ngrok.kill(); // kills ngrok process
'''

Note on http tunnels: by default bind_tls is true, so whenever you use http proto two tunnels are created - http and https. If you
 disconnect https tunnel, http tunnel remains open. You might want to close them both by passing http-version url, or simply by
disconnecting all in one go '''ngrok.disconnect()'''.

## emitter
...
```

#### <a name="apidoc.element.ngrok.kill"></a>[function <span class="apidocSignatureSpan">ngrok.</span>kill (cb)](#apidoc.element.ngrok.kill)
- description and source-code
```javascript
function kill(cb) {
	cb = cb || noop;
	if (!ngrok) {
		return cb();
	}
	ngrok.on('exit', function() {
		api = null;
		tunnels = {};
		emitter.emit('disconnect');
		return cb();
	});
	return ngrok.kill();
}
```
- example usage
```shell
...
Note on regions: region used in first tunnel will be used for all next tunnels too.

## disconnect
The ngrok and all tunnels will be killed when node process is done. To stop the tunnels use
'''javascript
ngrok.disconnect(url); // stops one
ngrok.disconnect(); // stops all
ngrok.kill(); // kills ngrok process
'''

Note on http tunnels: by default bind_tls is true, so whenever you use http proto two tunnels are created - http and https. If you
 disconnect https tunnel, http tunnel remains open. You might want to close them both by passing http-version url, or simply by
disconnecting all in one go '''ngrok.disconnect()'''.

## emitter
Also you can use ngrok as an event emitter, it fires "connect", "disconnect" and "error" events
'''javascript
...
```



# <a name="apidoc.module.ngrok._events"></a>[module ngrok._events](#apidoc.module.ngrok._events)

#### <a name="apidoc.element.ngrok._events.error"></a>[function <span class="apidocSignatureSpan">ngrok._events.</span>error ()](#apidoc.element.ngrok._events.error)
- description and source-code
```javascript
error = function () {}
```
- example usage
```shell
...
	freebsdx64:	cdn + cdnPath + 'freebsd-amd64.zip'
};

var arch = process.env.NGROK_ARCH || (os.platform() + os.arch());
var cdnFile = cdnFiles[arch];

if (!cdnFile) {
	console.error('ngrok - platform ' + arch + ' is not supported.');
	process.exit(1);
}

var localPath = __dirname + '/bin/';
var localFile = localPath + 'ngrok.zip';

console.log('ngrok - downloading binary ' + cdnFile + ' ...');
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
