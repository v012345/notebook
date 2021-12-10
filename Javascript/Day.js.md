[official documents](https://day.js.org/docs/en/installation/installation)

## [Now](https://day.js.org/docs/en/parse/now)
Calling dayjs() without parameters returns a fresh Day.js object with the current date and time.

```javascript
var now = dayjs()
```

This is essentially the same as calling dayjs(new Date()).

Day.js treats dayjs(undefined) as dayjs() due to that function parameters default to undefined when not passed in.

Day.js treats dayjs(null) as an invalid input.