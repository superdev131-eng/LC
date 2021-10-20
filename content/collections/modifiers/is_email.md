---
id: 471b3281-4573-43ee-9fee-eb55edf26ad0
blueprint: modifiers
modifier_types:
  - string
  - conditions
title: 'Is Email'
---
Returns `true` if a string is a valid email address.

```yaml
an_email: lknope@inpra.org
not_an_email: waffles
```

```
{{ if an_email | is_email }}
{{ if not_an_email | is_email }}
```

```html
true
false
```


