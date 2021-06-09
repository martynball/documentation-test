<!-- Space: WE -->
<!-- Parent: Web Documentation -->
<!-- Parent: Other -->
<!-- Title: Mix Fixes -->
<!-- Layout: (plain) -->

# Mix Fixes
This page has got a mixture of little fixes.

<a name="accordian"></a>
## Accordian
An issue was raised where on some mobiles, expanding an accordian can sometimes scroll the visitor down to the gallery or away from the content.
The code below should be merged with your `accordian` script within your custom javascript.

```javascript
$(selector).accordion({
    activate: function (event, ui) {
        let bounding = event.target.getBoundingClientRect();
        let scrollTop = window.pageYOffset || document.documentElement.scrollTop;
        if (bounding.top < 0) {
            document.documentElement.scrollTop = bounding.top + scrollTop;
        }
    }
});
```
