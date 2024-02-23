# PostgreSQL with PGlite

```js echo
const sql = view(Inputs.textarea({value: "select 'Hello world'", label: "SQL"}))
```
## Query result
```js
html`<pre>${JSON.stringify(response, null, 4)}</pre>`
```
## How this works
```js echo
import { PGlite } from "npm:@electric-sql/pglite@0.0.1-alpha.2/dist/index.min.js";
```
```js echo
const db = new PGlite
```
```js echo
const response = await db.query(sql)
```
