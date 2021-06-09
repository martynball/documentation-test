<!-- Space: WE -->
<!-- Parent: Web Documentation -->
<!-- Parent: Vue Components -->
<!-- Title: Favourites Panel -->
<!-- Layout: (plain) -->

# Favourites Panel

This panel will display vehicles which have been added to your favourites. Simply add the below HTML Tag to your HTML where you want it to display, ensure that you have got Vue enabled on the website.

```html
<favourites-panel class="app"></favourites-panel>
```

If you're adding this to a detail page, or have access to a vehicle ID, you can add this to the tag. This will add the **Add Vehicle** button to the panel to quickly add the vehicle.

```html
<favourites-panel class="app" vehicle-id='000000'></favourites-panel>
```

<a name="override-styles"></a>
## Override Styles
If you need to over-ride the styles then add `:custom-css="true"` to the HTML Tag, e.g:
```html
<favourites-panel class="app" :custom-css="true"></favourites-panel>
```
This will add `custom-css` class to the parent div which you can use to create a stronger target to the elements so you can avoid needing to use `!important`.

This is required as the component styles are added below the **theme** so they will take precedence over the theme without this.

<a name="override-slots"></a>
## Override Slots
There are multiple slots which can be used to over-ride sections of this component. These slots are used as follows where `name` is the name of the slot:
```html
<favourites-panel class="app" :custom-css="true">
    <template v-slot:name="props">
        
    </template>
</favourites-panel>
```
You can see the data within `props` by putting `{\{ props }\}` within the template and reloading the page.

Note: Remove the backslash from the braces above.

<a name="slots"></a>
## Slots:
- header
- no-vehicles-selected
- listing-not-found
- listing-image
- listing-title
- listing-title-header
- listing-title-subtitle
- listing-title-price
- listing-title-finance
- listing-title-favourites
- listing-summary
- listing-finance
- listing-info
- listing-location
- listing-cta
- listing-add-current

Below is the HTML to create the `favourites-panel-finance` component as an example of how to use the slots:
```html
<favourites-panel class="app">

    <template v-slot:listing-title-finance><span style="height:0;display: block;"></span></template>
    <template v-slot:listing-info><span style="height:0;display: block;"></span></template>
    <template v-slot:listing-finance="props">
        <div class="vehicle-listing__finance">
            <div class="results_monthly_payment">
                <div class="finance-presentation">
                    <div class="finance-presentation__payments">
                        <em class="finance-presentation__deposit">£{\{ props.vehicle.deposit }} <span>deposit</span></em>
                        <i class="ci ci-plus"></i>
                        <em class="finance-presentation__monthly-payment">£{\{ props.vehicle.minimum_payment }} <span>per month</span></em>
                    </div>
                </div>
            </div>
        </div>
    </template>
</favourites-panel>
```
