---
modifier_types:
  - date
  - conditions
id: bd468407-617a-4cb8-93d8-cfd7148ec157
parse_content: true
---
Returns `true` if date is yesterday - using the server's time.

```.language-yaml
date: {{ now modify_date="-1 day" format="F j Y" }}
```
{{ noparse }}
```
{{ if date | is_yesterday }}
```
{{ /noparse }}

```.language-output
true
```
