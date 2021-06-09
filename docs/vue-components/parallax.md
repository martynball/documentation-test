<!-- Space: ~213834277 -->
<!-- Parent: Web Documentation -->
<!-- Parent: Vue Components -->
<!-- Title: Parallax -->
<!-- Layout: (plain) -->

# Parallax

This Parallax component allows you to have multiple levels of parallax. Due to the effect being applied to `div`'s you can also apply the parallax effect to text and any other content.

<a name="useage"></a>
## Usage

Pretty simple to use, simply add the `<parallax>` HTML tag to your HTML, and then add your layers and any static content.

> {note} In order for the layer to function correctly only change `layer--one` class name, you change this to what ever you want as this is just used by you to define the background image within your theme.

You can add other HTML into the parallax layer as well as the overlay.

You can create effects like [this](http://www.firewatchgame.com/) if you create the right images.

[Live Example](http://devsite301.clickserver.co.uk/parallax-example.php)

<a name="example-html"></a>
## Example HTML
```html
<parallax class="app parallax--about">
    <div class="overlay">
        <h1>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</h1>
        <p>Nulla est sapien, vestibulum nec suscipit in, vulputate sit amet augue. Proin enim urna, congue a tempor sit amet, hendrerit at diam. Quisque iaculis sagittis hendrerit. Suspendisse sagittis mauris elit, non suscipit metus venenatis eu.</p>
    </div>
    <div class="layer layer--one" data-layer data-depth="0.8" v-in-viewport></div>
</parallax>
```

<a name="example-less"></a>
## Example LESS
```css
.parallax--about {
  & > .overlay {
    padding: 40px;
    background: rgba(0,0,0,.5);
    h1, p {
      color: #fff;
    }
  }
  & > .layer--one.in-viewport {
    background-image: url('@{dealer-img}/theme/parallax-background-1.jpg');
    @media @tablet {
      background-image: url('@{dealer-img}/theme/parallax-background-1--tablet.jpg');
    }
    @media @mobile {
      background-image: url('@{dealer-img}/theme/parallax-background-1--mobile.jpg');
    }
  }
}
```

Stick with the class names as the component has got base styles within it to make the effect function.

<a name="settings"></a>
## Settings
- data-depth: This defined the speed the parallex effect scrolls the layer, the lower the number the slower it goes.
- data-layer: This is required to define the `div` as a parallax layer.
- v-in-viewport: This is also required, this simply adds lazy loading to the images. 
