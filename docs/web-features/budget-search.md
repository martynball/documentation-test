<!-- Space: WE -->
<!-- Parent: Web Documentation -->
<!-- Parent: Web Features -->
<!-- Title: Budget Search -->
<!-- Layout: (plain) -->

# Budget Search

If you have a custom template for your homepage search then this will be missing the vehicle type, so the **Make** count will be ALL vehicle types.

This causes more to be potentially shown if the dealer also has vars/bikes as additional vehicles type. Add the below the `form` opening tag.

## Before:
```html
<form method="get" action="/search_page.php">

    <input type="hidden" id="search-instance" value="{{ instance }}">
    <input type='hidden' value='0' name='budgetswitch'>
    ...
```

## After:
```html
<form method="get" action="/search_page.php">

    {% if 'vehicle_type' not in fields|keys %}<input type='hidden' value='{{ vehicle_type }}' name='vehicle_type'>{% endif %}
    <input type="hidden" id="search-instance" value="{{ instance }}">
    <input type='hidden' value='0' name='budgetswitch'>
    ...
```
