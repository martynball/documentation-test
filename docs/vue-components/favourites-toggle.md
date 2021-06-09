<!-- Space: WE -->
<!-- Parent: Web Documentation -->
<!-- Parent: Vue Components -->
<!-- Title: Favourites Toggle -->
<!-- Layout: (plain) -->

# Favourites Toggle

This component will add a toggle to your website, this should be used within the search page under each vehicle listing.

Simply replace the `1234` within the **vehicle-id** below with the vehicle's ID, then this will be added to the favourites when clicked.

```html
<favourites-toggle class="app" vehicle-id="1234"></favourites-toggle>
```

<a name="override-html"></a>
## Override HTML
To override the html within the component you can use the below code and modify to your needs.

```html
<favourites-toggle class="app" vehicle-id="{DETAIL_ID}">
    <template v-slot:default="slotProps">
        <a href="javascript:void(0)"
           title="Add to favourites"
           @click="slotProps.toggle()"
           :class="{ 'favourites-added': slotProps.added }"><i :class="{ 'ci ci-heart-r': !slotProps.added, 'ci ci-heart': slotProps.added }"></i></a>
    </template>
</favourites-toggle>
```
