# PyPI download stats for Datasette projects

Showing downloads for **${packageName}**

```js echo
const packageName = view(Inputs.select(packages, {
  value: "sqlite-utils",
  label: "Package"
}));
```
```js echo
Plot.plot({
  y: {
    grid: true,
    label: `${packageName} PyPI downloads per day`
  },
  width: width,
  marginLeft: 60,
  marks: [
    Plot.line(data_with_dates, {
      x: "date",
      y: "downloads",
      title: "downloads",
      tip: true
    })
  ]
})
```
## Fetch statistics for selected package
```js echo
const data = d3.json(
  `https://datasette.io/content/stats.json?_size=max&package=${packageName}&_sort_desc=date&_shape=array`
);
```
```js echo
const data_with_dates = data.map(function(d) {
  d.date = d3.timeParse("%Y-%m-%d")(d.date);
  return d;
})
```
```js echo
Inputs.table(data_with_dates)
```
## Fetch list of packages
```js echo
const packages_sql = "select package from stats group by package order by max(downloads) desc"
```
```js echo
const packages = fetch(
  `https://datasette.io/content.json?sql=${encodeURIComponent(
    packages_sql
  )}&_size=max&_shape=arrayfirst`
).then((r) => r.json());
```
```js echo
packages
```
