---
id: ada24ec2-1b6e-4759-b2c0-06d9d464f3f9
modifier_types:
  - array
  - utility
---
Alias an array variable with a key, giving you some useful markup/iteration options.

```.language-yaml
blocks:
  -
    type: text
    content: I love to eat tacos in the bathroom.
  -
    type: photo
    photo: /assets/img/baño-tacos.jpg
```

```
{{ blocks as="block" }}
  {{ block | partial:type }}
{{ /blocks }}
```

```.language-output
<!-- Each block would be rendered with its own partial matching the {{ type }} var -->

<div class="text">
  <p>I like to eat tacos in the bathroom.</p>
</div>
<div class="photo">
  <img src="/assets/img/baño-tacos.jpg">
</div>
```
