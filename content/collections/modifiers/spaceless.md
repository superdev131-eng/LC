---
modifier_types:
  - string
  - utility
added_in: 2.8.4
id: 3bcdbffa-8020-4364-8c2a-1fe1a9ff0a5c
---
Removes excess whitespace and line breaks from a string. A definite OCD pleaser.

```
html: |
    <p>I copy & pasted
        <a href="http://goodnightchrome.show">this link
        </a>   <strong>for you!</strong>    </p>
```

```
{{ html | spaceless }}
```

```.language-output
<p>I copy & pasted <a href="http://goodnightchrome.show">this link </a><strong>for you!</strong></p>
```
