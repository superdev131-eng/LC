---
types:
  - condition
id: e08b1034-5d58-4fae-8f6a-8efd9a65d6d9
---
Search a string against multiple needles and return `true` if all are found, otherwise `false`. Case-insensitive.

```.language-yaml
summary: "It was the best of times, it was the worst of times."
```

```
{{ if summary | contains_all:best:worst }}
{{ if summary | contains_all:best:better }}
```

```.language-output
true
false
```
