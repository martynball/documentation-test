<!-- Space: WE -->
<!-- Parent: Web Documentation -->
<!-- Parent: Vue Components -->
<!-- Title: Favourites Counter -->
<!-- Layout: (plain) -->

# Favourites Counter

This component will add a favourites counter to your website, this counter will also be a link to the gallery page.

```html
<favourites-counter class="app"></favourites-counter>
```

> {tip} We noticed a lot of the time you guys simply want to remove the text from this component, from so now on please simply add the ```text``` property like so: ```html <favourites-counter class="app" text=""></favourites-counter> ```

<a name="override-html"></a>
## Override HTML

You can override the component HTML by using the below code.

```html
<favourites-counter class="app header__favourites">
    <template v-slot:default="slotProps">
        <a href="/compare.php" title="View your saved cars"><span class="favourites-count">\{\{ slotProps.count \}\}</span> Saved Cars</a>
    </template>
</favourites-counter>
```

> {note} Remove the backward slashes from the curly braces!
