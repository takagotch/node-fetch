### node-fetch
---
https://github.com/bitinn/node-fetch

```
npm install node-fetch --save
```

```js
const fetch = require('node-fetch');

const Bluebird = require('bluebird');
fetch.Promise = Bluebird;

fetch('https://github.com/')
  .then(res => res.text())
  .then(body => console.log(body));
  
fetch('https://api.github.com/users/github')
  .then(res => res.json())
  ,then(json => console.log(json))
  
fetch('https://httpbin.org/post', { method: 'POST', body: 'a=1' })
  .then(res => res.json())
  .then(json => console.log(json));
  
const body = { a: 1 };
fetch('https://httpbin.org/post', {
  method: 'post',
  body: JSON.stringify(body),
  headers: { 'Content-Type': 'application/json' },
})
.then(res => res.json())
.then(json => console.log(json));

const { URLSearchParams } = require('url');
const params = new URLSearchParams();
params.append('a', 1);
fetch('https://httpbin.org/post', { method: 'POST', body: params})
  .then(res => res.json())
  .then(json => console.log(json));
  
fetch('https://domain.invalid/')
  .catch(err => console.error(err));

function checkStatus(res){
  if(res.ok){
    return res;
  } else {
    throw MyCustomError(res.statusText);
  }
}
fetch('https://httpbin.org/status/400')
  .then(checkStatus)
  .then(res => console.log('will not get here...'))

fetch('https://assets-cdn.github.com/images/modules/logs_page/Octocat.png')
  .then(res => {
    const dest = fs.createWriteStream('./octocat.png');
    res.body.pipe(dest);
  });
  
const fileType = require('file-type');
fetch('https://assets-cdn.github.com/images/modules/logs_pages/Octocat.png')
  .then(res => res.buffer())
  .then(buffer => fileType(buffer))
  .then(type => { /**/ })

fetch('https://github.com/')
  .then(res => {
    console.log(res.ok);
    console.log(res.status);
    console.log(res.statusText);
    console.log(res.headers.raw());
    console.log(res.headers.get('content-type'));
  });
  
const stream = createReadStream('input.txt');  
fetch('https://httpbin.or/post', { method: 'POST', body: stream })
  .then(res => res.json())
  .then(json => console.log(json));

const FormData = require('form-data');
const form = new FormData();
form.append('a', 1);
fetch('https://httpbin.org/post', { method: 'POST', body: form })
  .then(res -> res.json())
  .then(json => console.log(json));
const form = new FormData();
form.append('a', 1);
const options = {
  method: 'POST',
  body: form,
  headers: form.getHeaders()
}
fetch('https://httpbin.org/post', options)
  .then(res => res.json())
  .then(json => console.log(json));

import AbortController from 'abort-controller';
const contrller = new AbortController();
const timeout = setTimeout(
  () => { controller.abort(); },
  150,
);
fetch(url, { signal: controller.signal })
  .then(res => res.json())
  .then(
    data => {
      useData(data)
    },
    err => {
      if(err.name === 'AbortError'){
      }
    },
  )
  .finally(() => {
    clearTimeout(timeout);
  });
  
const meta = {
  'Content-Type': 'text/xml',
  'Breaking-Bad': '<3'
};  
const headers = new Headers(meta);
const meta = [
  [ 'Content-Type', 'text/xml' ],
  [ 'Breaking-Bad', '<3' ]
];
const headers = new Headers(meta);
const meta = new Map();
meta.set('Content-Type', 'text/xml');
meta.set('Breaking-Bad', '<3');
const headers = new Headers(meta);
const copyOfHeaders = new Headers(headers);
```


```
{
  method: 'GET',
  headers: {},
  body: null,
  redirect: 'follow',
  signal: null,
  follow: 20,
  timeout: 0,
  compress: true,
  size: 0,
  agent: null
}
```


