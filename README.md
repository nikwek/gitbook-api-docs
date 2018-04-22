# Hello World

## Testing GitBook for API docs

Supports Markdown with neat features

```
$ give me super-powers
```

### Hint

Available styles are:

- info (default)
- tip
- danger
- working

{% hint style='info' %}
Important info: this note needs to be highlighted
{% endhint %}

{% hint style='tip' %}
Tip: this note needs to be highlighted
{% endhint %}

{% hint style='danger' %}
Danger: this note needs to be highlighted
{% endhint %}

{% hint style='working' %}
Working: this note needs to be highlighted
{% endhint %}

### Code Tabs

This is a code block with tabs for each languages:

{% codetabs name="Python", type="py" -%}
msg = "Hello World"
print msg
{%- language name="JavaScript", type="js" -%}
var msg = "Hello World";
console.log(msg);
{%- language name="HTML", type="html" -%}
<b>Hello World</b>
{%- endcodetabs %}