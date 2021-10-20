---
id: 18596c62-5535-41a8-91c4-b5769fb11085
blueprint: modifiers
modifier_types:
  - date
parse_content: true
title: 'Modify Date'
---
Alters a timestamp by incrementing or decrementing in a format accepted by PHP's native [`strtotime()`](http://php.net/manual/en/function.strtotime.php) method.


```yaml
date: {{ now }}
```

{{ noparse }}
```
{{ date | modify_date:last Sunday }}
{{ date | modify_date:+3 months }}
{{ date | modify_date:-2 weeks }}
```
{{ /noparse }}

```html
{{ now | modify_date:last Sunday }}
{{ now | modify_date:+3 months }}
{{ now | modify_date:-2 weeks }}
```

:::tip
This modifier **modifies the variable directly** which will carry over to subsequent modifications, as shown in the above example.
:::
