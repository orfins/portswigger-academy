I tried to play with some events in the search bar, and I found that this one works in earlier labs because `<body>` is not blocked:

```html
<body onload="alert();">random text</body>
```

But `onload` is not run when used on a custom tag:

```html
<custom onload="alert();">random text</custom>
```

So I need to find some other event that is triggered. I found that `onmouseover` works when I put my mouse  
over the text:

```html
<custom onmouseover="alert();">random text</custom>
```

So the conclusion is that some events indeed work with custom tags,  
although the bot won't hover over the text so I can't use `onmouseover`.

So I tested some other stuff from this list: https://www.w3schools.com/tags/ref_eventattributes.asp

None of the "Window Event Attributes" seemed to work, and obviously nothing that requires manual  
user input is of use to me.

Under "Form Events", again, nothing seemed to work, except that I don't know what "element gets focused" means:
> onfocus	script	Fires the moment when the element gets focus

So I googled:
> how to focus on element without javascript

And found https://www.w3schools.com/tags/att_input_autofocus.asp#:~:text=The%20autofocus%20attribute%20is%20a,focus%20when%20the%20page%20loads.

It looks like autofocus works with `<input>`, so I gave this a try anyway:

```html
<custom onfocus="alert();" autofocus>
```

But it failed. So I googled:
> autofocus with custom tag

And found this: https://stackoverflow.com/a/52437469

And then I tried:

```html
<custom onfocus="alert();" tabindex="-1" autofocus>
```

Which finally worked. I then read a bit more about `tabindex` to know what it does.

I tried this as my final answer:

```html
<custom onfocus="alert(document.cookie);" tabindex=1 autofocus>
```

But for some reason it worked with "View exploit" and entering the `/exploit` url manually,  
but not with "Deliver exploit to victim".

I looked at the given solution, and it seems that I was supposed to redirect the viction to a `/search` result.

Final answer:

```html
<script>
    location ='https://ac421f981e06292a80d62d980066001c.web-security-academy.net/?search=<custom onfocus="alert(document.cookie);" tabindex=1 autofocus>'
</script>
```

Also apparently instead of `/?search=<custom ... autofocus>` I could have also done `/?search=<custom ... >#custom`. Now I know how the `#` in the end of urls actually works.