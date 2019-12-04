---
title: Translate
intro: |
  Retrieve a string from a language file in the current locale. It is the equivalent of the [trans and trans_choice methods](https://laravel.com/docs/6.x/localization) provided by Laravel.
parameters:
  -
    name: key
    type: tagpart|string
    description: 'The key of the translation string to find. Include both the filename and string key delimited with dots. Can be used as a tag part or a `key` parameter. If your key contains a namespace, you should use the key parameter instead of the tag part.'
  -
    name: 'any parameters'
    type: string
    description: 'Any additional parameters will be treated as parameters that should be replaced in the string.'
  -
    name: count
    type: 'integer *1*'
    description: 'When using `trans_choice`, this is the number that defines the pluralization.'
id: 8ff99539-8b1a-4380-adf7-bdad979f8afd
stage: 4
---

> There's also a [modifier](/modifiers/trans) version that you may prefer.

## Usage {#usage}

Get the `bar` string from the `resources/lang/en/foo.php` translation file (where `en` is the current locale).

``` .language-php
<?php
return [
    'bar' => 'Bar!',
    'welcome' => 'Welcome, :name!',
    'apples' => 'There is one apple|There are :count apples',
];
```

```
{{ trans:foo.bar }} or {{ trans key="foo.bar" }}
```

``` .language-output
Bar!
```

## Replacements

Any additional tag parameters will be treated as parameters that should be replaced in the string. 

```
{{ trans:foo.welcome name="Bob" }}
```

``` .language-output
Welcome, Bob!
```

## Pluralization {#pluralization}

To pluralize, use the `trans_choice` tag with a `count` parameter.

```
{{ trans_choice:foo.apples count="2" }}
```

``` .language-output
There are 2 apples
```
