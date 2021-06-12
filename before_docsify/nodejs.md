# Installing Node
Lo más fácil es usar [NVM](https://github.com/creationix/nvm).
Note: you can use an .nvmrc file to choose a default nvm version.
https://github.com/creationix/nvm#nvmrc

# Learning Node Basics

[The Node Begginer Book](http://www.nodebeginner.org/) (gratis)

[Learning Node](http://shop.oreilly.com/product/0636920024606.do) ($28)

[7 tips for a Node.js padawan](https://medium.com/tech-talk/e7c0b0e5ce3c)

[Package.json dependencies done right](http://blog.nodejitsu.com/package-dependencies-done-right)

# Build tools

[Using Grunts config API](http://www.integralist.co.uk/posts/using-grunts-config-api/)

[Why we should stop using Grunt &amp; Gulp](http://blog.keithcirkel.co.uk/why-we-should-stop-using-grunt/)

[How to Use npm as a Build Tool](https://www.keithcirkel.co.uk/how-to-use-npm-as-a-build-tool/)

# Organizing your projects

[Building Modular Express apps](http://vimeo.com/56166857)

# Databases

[Massive](https://github.com/robconery/massive-js) - A simple relational data access tool for NodeJS.

[node-postgres](https://github.com/brianc/node-postgres) - PostgreSQL client for node.js.

[db-migrate](https://db-migrate.readthedocs.io/en/latest/) - Database migration framework for node.js

[Graffiti](https://github.com/RisingStack/graffiti) - Node.js GraphQL ORM

# Testing / Mocking

[chai](http://chaijs.com/) - BDD / TDD assertion library for [node](http://nodejs.org/) and the browser that can be delightfully paired with any javascript testing framework.

[Sinon.JS](http://sinonjs.org/) - Standalone test spies, stubs and mocks for JavaScript.

[nock](https://github.com/node-nock/nock) - HTTP mocking and expectations library

[mocha](https://mochajs.org/) -  feature-rich JavaScript test framework

[jasmine](http://jasmine.github.io/) - Behaviour-Driven Javascript

[pact](https://docs.pact.io/) - consumer driven contract testing

[nightwatch](http://nightwatchjs.org/) - Browser automated testing done easy.

[dalekjs](http://dalekjs.com/) - Automated cross browser testing with Javascript!

[Chakram](http://dareid.github.io/chakram/) - REST API testing framework offering a BDD testing style and fully exploiting promises

[BackstopJS](https://garris.github.io/BackstopJS/) - breaking CSS is easy. Checking every responsive page element is hard. That&#39;s why there&#39;s BackstopJS.

# Authentication

[JSON web token](https://github.com/auth0/node-jsonwebtoken) - JsonWebToken implementation for node.js

[passportjs](http://passportjs.org/) - Simple, unobtrusive authentication for Node.js

# HTTP requests

[superagent](https://github.com/visionmedia/superagent) - Ajax with less suck - (and node.js HTTP client to match)

# JSON Schema

[jayschema](https://github.com/natesilva/jayschema) - comprehensive [JSON Schema](http://json-schema.org/) validator for Node.js

# Security

[helmet](https://github.com/evilpacket/helmet) - Collection of middleware to implement various security headers for Express / Connect

[csrf](http://www.senchalabs.org/connect/csrf.html) - connect native middleware to prevent cross site request forgery

[CSP](https://developer.mozilla.org/en-US/docs/Web/Security/CSP) - Content Security Policy

http://cspisawesome.com/

http://githubengineering.com/subresource-integrity/


# Logging

[winston](https://github.com/flatiron/winston) - a multi-transport async logging library for node.js

https://papertrailapp.com/

[debug](https://github.com/visionmedia/debug) - tiny node.js & browser debugging utility for your libraries and applications

# Debugging

[Debugging in Chrome Dev Tools](https://medium.com/@paul_irish/debugging-node-js-nightlies-with-chrome-devtools-7c4a1b95ae27)

[node-inspector](https://github.com/dannycoates/node-inspector) - Web Inspector based nodeJS debugger

[Ghostlab](http://vanamco.com/ghostlab/) - Kick-ass synchronized website development. Inspect/Debug your code on any connected device remotely.

[Samsung RemoteTestLab](http://developer.samsung.com/remotetestlab) - enables developers to access Samsung mobile devices through the web and to install and test applications on the devices

- To debug using the built-in `node inspect`:
  ```
  node --inspect-brk myapp.js
  ```

  On a separate terminal:
  ```
  node inspect localhost:9229
  ```

  Debug commands:
  - `cont`, `c`: Continue execution
  - `next`, `n`: Step next
  - `step`, `s`: Step in
  - `out` , `o`: Step out

  https://nodejs.org/api/debugger.html#debugger_command_reference

# Business Metrics

https://mixpanel.com/

https://mixpanel.com/blog/2012/11/15/aarrr-mixpanel-for-pirates/

https://mixpanel.com/blog/2012/11/13/getting-serious-about-measuring-virality/

https://kissmetrics.com/

https://segment.com/

https://keen.io/

http://piratemetrics.com/

# Monitoring / Performance
También se le llama APM (Application Performance Monitoring)

https://keymetrics.io

http://www.appdynamics.com/nodejs/

http://newrelic.com/nodejs

https://ruxit.com/

[PSI](http://addyosmani.com/blog/automating-web-performance-measurement-with-psi-for-node/) - Page Speed Insights for your node app

On the frontend:

https://trackjs.com/

https://raygun.io/

# User Feedback

https://doorbell.io/

http://userecho.com/

https://www.groovehq.com

# Docker

https://blog.codeship.com/using-docker-compose-for-nodejs-development/

# Deployment

[A Guide to Creating a NodeJS Command-Line Package](https://x-team.com/blog/a-guide-to-creating-a-nodejs-command/)
Follow this guide when publishing a cli tool to npm

[Dokku](http://progrium.viewdocs.io/dokku/index) - your own, single-host version of Heroku (ver [post](http://progrium.com/blog/2013/06/19/dokku-the-smallest-paas-implementation-youve-ever-seen/))

[How to deploy your node app on Linux, 2016 edition](https://certsimple.com/blog/deploy-node-on-linux)

[How To Use PM2 to Setup a Node.js Production Environment On An Ubuntu VPS](https://www.digitalocean.com/community/tutorials/how-to-use-pm2-to-setup-a-node-js-production-environment-on-an-ubuntu-vps)

[Node.js Production Environment - a Step-By-Step Guide for Startups](https://blog.risingstack.com/nodejs-production-environment-for-startups)

# Robotics

http://johnny-five.io/
https://github.com/dtex/tharp
http://www.seeedstudio.com/depot/ARDX-The-starter-kit-for-Arduino-p-1153.html

# CLI apps
- [yargs](https://github.com/yargs/yargs)
  build interactive command line tools, by parsing arguments and generating an elegant user interface

# Streams
Docs: https://nodejs.org/docs/latest-v14.x/api/stream.html

## Where to get a stream

You can create a stream by reading a file:
```javascript
const fs = require('fs');

// read from a file
fs.createReadStream('./my-source-file');

// write to a file
fs.createWriteStream('./my-dest-file');
```

You can get a stream from stdin (eg: `cat my-source-file | my-node-app`):
```javascript
process.stdin.pipe(process.stdout);
```

## How to write a Tranform stream

```javascript
#!/usr/bin/env node

const split2 = require('split2');
const { Transform } = require('stream');

// filter out duplicate chunks
class Unique extends Transform {
  constructor(options) {
    super(options);
    this.memo = {};
  }

  _transform(chunk, enc, callback) {
    const str = chunk.toString();
    if (this.memo[str]) {
      return callback();
    }
    this.memo[str] = 1;
    this.push(`${str}\n`);
    return callback();
  }
}

process.stdin
.pipe(split2())
.pipe(new Unique())
.pipe(process.stdout);
```

# Linting
[ESLint](http://www.smashingmagazine.com/2015/09/eslint-the-next-generation-javascript-linter)
[ESLint + Prettier](https://prettier.io/docs/en/eslint.html)
  ```
  # add dependencies
  npm install --save-dev prettier eslint
  npm install --save-dev eslint-config-prettier
  npx install-peerdeps --dev eslint-config-airbnb

  # example .eslintrc.json
  {
    "env": {
      "browser": true
    },
    "extends": ["airbnb", "prettier"]
  }
  ```

# Other

[Composition over inheritance](https://www.youtube.com/watch?v=wfMtDGfHWpA)

[Simple Recommendation Engine in Javascript](https://medium.com/@keithwhor/using-graph-theory-to-build-a-simple-recommendation-engine-in-javascript-ec43394b35a3)

[supporting both CommonJS and AMD](https://github.com/umdjs/umd)
[hashid](http://www.hashids.org/) - Generate short hashes from numbers (like YouTube and Bitly)

[limit](http://www.senchalabs.org/connect/limit.html) | [rawbody](https://github.com/stream-utils/raw-body) - connect middleware to limit request body size

[node-toobusy](https://github.com/lloyd/node-toobusy) - prevent node's main process to become saturated

[cron](https://www.npmjs.com/package/cron) - Cron jobs for your node

[charles](http://www.charlesproxy.com/) - web debugging proxy application

[ngrok](https://ngrok.com/) -  ngrok creates a secure public URL (https://yourapp.ngrok.io) to a local webserver on your machine

[CSS modules](http://glenmaddern.com/articles/css-modules)
