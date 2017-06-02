# Serville

Serville is a **fast, tiny, and opinionated** HTTP library for NodeJS.
Ideal for APIs, it serves up JSON and nothing but JSON.

**Installing:**

```sh
npm i --save serville
```

**Using:**

```js
const app = require('serville')();
app.listen('8080');
```

**Basic Listening:**

```js
app.at('/', (q) => ({ message: "Hello!" }));
// GET localhost:8080/
// => { "message": "Hello!" }
```

**URL Parameters:**

```js
app.at('/say/:text', (q) => ({ text: q.params.text }));
// GET localhost:8080/say/hello
// => { "text": "hello" }
```

**Optional Trailing Slash:**

```js
app.at('/either/way/?', (q) => ({ message: "Hey there! "}));
// GET localhost:8080/either/way
// => { "message": "Hey there!" }
// GET localhost:8080/either/way/
// => { "message": "Hey there!" }
```

**Returning Promises:**

```js
app.at('/delay/:secs', (q) => {
  return new Promise((res) => {
    setTimeout(() => {
      resolve({ result: "DONE" });
    }, q.params.secs * 1000);
  })
});
// GET localhost:8080/delay/10
// (10 second delay)
// => { "result": "done" }
```

**GET and POST queries:**

```js
app.at('/echo', (q) => ({ text: q.query.text }));
// GET localhost:8080/echo?text=Hello!
// => { "text": "Hello!" }
// POST localhost:8080/echo
// POST body: text=Hello!
// => { "text": "Hello!" }
```

**HTTP Request Headers:**
```js
app.at('/agent', (q) => ({ agent: q.headers['user-agent'] }));
```

## Contributing

Fork and clone this repository to get started, then run `npm i` to install dev
dependencies.
There's no formal contribution procedure (yet), feel free to submit PRs and issues as you see
fit. Contributions are very much welcomed!

The source code for the library is in `dev/serville.js`.
Modify the testing script in `dev/test.js` to try out your changes and new
features. You can run these tests with `npm test`.

To build the current version of the server to `serville.js`, simply run `npm run build`.