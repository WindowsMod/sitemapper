## Sitemap-parser

Parse through a sitemaps xml to get all the urls for your crawler.
## Version 3

### Installation
```bash
npm i @wmod/sitemapper
```

### Simple Example
```javascript
const Sitemapper = require('sitemapper');

const sitemap = new Sitemapper();

sitemap.fetch('https://wp.seantburke.com/sitemap.xml').then(function(sites) {
  console.log(sites);
});

```
### Examples in ES6
```javascript
import Sitemapper from 'sitemapper';

(async () => {
  const Google = new Sitemapper({
    url: 'https://www.google.com/work/sitemap.xml',
    timeout: 15000, // 15 seconds
  });

  try {
    const { sites } = await Google.fetch();
    console.log(sites);
  } catch (error) {
    console.log(error);
  }
})();

// or

const sitemapper = new Sitemapper();
sitemapper.timeout = 5000;

sitemapper.fetch('https://wp.seantburke.com/sitemap.xml')
  .then(({ url, sites }) => console.log(`url:${url}`, 'sites:', sites))
  .catch(error => console.log(error));
```

# Options

You can add options on the initial Sitemapper object when instantiating it.

+ `requestHeaders`: (Object) - Additional Request Headers (e.g. `User-Agent`)
+ `timeout`: (Number) - Maximum timeout in ms for a single URL. Default: 15000 (15 seconds)
+ `url`: (String) - Sitemap URL to crawl
+ `debug`: (Boolean) - Enables/Disables debug console logging. Default: False
+ `concurrency`: (Number) - Sets the maximum number of concurrent sitemap crawling threads. Default: 10
+ `retries`: (Number) - Sets the maximum number of retries to attempt in case of an error response (e.g. 404 or Timeout). Default: 0
+ `rejectUnauthorized`: (Boolean) - If true, it will throw on invalid certificates, such as expired or self-signed ones. Default: True
+ `lastmod`: (Number) - Timestamp of the minimum lastmod value allowed for returned urls
+ `field`: (Object) - An object of fields to be returned from the sitemap. For Example: `{ loc: true, lastmod: true, changefreq: true, priority: true }`. Leaving a field out has the same effect as `field: false`. If not specified sitemapper defaults to returning the 'classic' array of urls.
+ `limitElements`: (Number) - Trim the output of the contents of the URL array to some limit

```javascript

const sitemapper = new Sitemapper({
  url: 'https://art-works.community/sitemap.xml',
  rejectUnauthorized: true,
  timeout: 15000,
  requestHeaders: {
    'User-Agent': 'Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:81.0) Gecko/20100101 Firefox/81.0'
  }
});

```

An example using all available options:

```javascript

const sitemapper = new Sitemapper({
  url: 'https://art-works.community/sitemap.xml',
  timeout: 15000,
  requestHeaders: {
    'User-Agent': 'Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:81.0) Gecko/20100101 Firefox/81.0'
  },
  debug: true,
  concurrency: 2,
  retries: 1,
  limitElements: 10,
});

```

### Examples in ES5
```javascript
var Sitemapper = require('sitemapper');

var Google = new Sitemapper({
  url: 'https://www.google.com/work/sitemap.xml',
  timeout: 15000 //15 seconds
});

Google.fetch()
  .then(function (data) {
    console.log(data);
  })
  .catch(function (error) {
    console.log(error);
  });


// or


var sitemapper = new Sitemapper();

sitemapper.timeout = 5000;
sitemapper.fetch('https://wp.seantburke.com/sitemap.xml')
  .then(function (data) {
    console.log(data);
  })
  .catch(function (error) {
    console.log(error);
  });

```

## Version 1

```bash
npm install sitemapper@1.1.1 --save
```

### Simple Example

```javascript
var Sitemapper = require('sitemapper');

var sitemapper = new Sitemapper();

sitemapper.getSites('https://wp.seantburke.com/sitemap.xml', function(err, sites) {
    if (!err) {
     console.log(sites);
    }
});
```
