---
theme: dashboard
---

# Observable Framework Experiments

Markdown content goes here.

This will output 1870:

```js
34 * 55
```

Use `js echo` as the tag and the code is output too:

```js echo
34 * 55
```

Here's the current date and time, updating constantly:

```js
new Date(now)
```

The same thing as an inline string: ${new Date(now)}

## Fetching data

`fetch()` can be used to fetch data. Here's recent Datasette news:

```js echo
const news = await fetch(
  "https://datasette.io/content/news.json?_shape=array"
).then(r => r.json())
```
Outputting just `news` displays the data with an interactive object explorer:
```js echo
news
```
Or use `Inputs.table()` to show it as a table. I filtered out the `rowid` column here:
```js echo
Inputs.table(news.map(({ rowid, ...rest }) => rest))
```
Let's display the most recent three items directly, using the `html` tag in a JavaScript block:

```js echo
html`
<h2>Latest Datasette news</h2>
<blockquote>
  ${news.slice(0, 3).map(
    item => html`<h3>${item.date}</h3>
      ${html({raw: [parse(item.body)]})}</p>`)
  }
</blockquote>
`
```

```js echo
import {parse} from "npm:marked";
```
