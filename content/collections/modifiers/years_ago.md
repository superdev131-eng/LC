---
id: e73f1574-732e-4a74-be47-37e1fddb05d6
blueprint: modifiers
modifier_types:
  - date
parse_content: true
title: 'Years Ago'
---
Returns the number of years since a given date variable. Statamic will attempt to parse any string as a date, but try to keep it in the least ambiguous date format possible.

```yaml
date: October 1 2015
```

{{ noparse }}
```
{{ date | years_ago }}
```
{{ /noparse }}

```html
{{ test_date | years_ago }}
```
