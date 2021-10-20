---
id: 396883d6-a3bc-4d98-a5a0-894e744b0451
blueprint: variables
types:
  - entry
title: 'Has Timestamp'
---
A boolean for whether or not an entry is time-based.

```
{{ if has_timestamp }}
    {{ date format="F jS, Y g:i a" }}
{{ else }}
    {{ date format="F jS, Y" }}
{{ /if }}
```

```html
January 1st, 2016 11:30 am
```
