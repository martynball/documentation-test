<!-- Space: WE -->
<!-- Parent: Web Documentation -->
<!-- Parent: Vue Components -->
<!-- Title: Slider -->
<!-- Layout: (plain) -->

# Slider

- [Using Endpoint](#using-endpoint)
- [Default with image format](#image-format)
- [Custom Slides](#custom-slides)
- [Custom Slides Loop](#custom-slides-loop)
- [Custom Slides with Endpoint](#custom-slides-endpoint)

The slider can be used in multiple ways. It is a wrapper around the [Swiper API](https://github.surmon.me/vue-awesome-swiper/), so any examples on there can be recreated using our `Slider`.

<a name="basic-usage"></a>
## Basic Usage
Using the `Default` slider from the link above, we would change the HTML from:
```html
<swiper class="swiper">
    <swiper-slide>Slide 1</swiper-slide>
    <swiper-slide>Slide 2</swiper-slide>
</swiper>
```
Change it to this:
```html
<slider class="app">
    <slide>Slide 1</slide>
    <slide>Slide 2</slide>
</slider>
```

<a name="settings"></a>
## Settings
All the same settings from `Swiper` can be applied to your slider, to apply your settings created within web planner you need to add the settings name, as follows:
```html
<slider class="app" name="custom-slider"></slider>
```

You can over-ride the default settings of global sliders, simply select which global slider from the dropdown.

<a name="using-endpoint"></a>
## Using Endpoint
Load images from an endpoint, the endpoint should return an `Array` of urls.
```html
<slider class="app" endpoint="/api/v1/vehicle-slider" vehicle-id="{DETAIL_ID}"></slider>
```

<a name="image-format"></a>
## Default with image format
Display # number of images from theme folder, default format is `slide-#`, however this can be changed as displayed below.
```html
<slider class="app" number-of-images="5" image-format="slide-#.jpg"></slider>
```

<a name="custom-slides"></a>
## Custom Slides
You can create complete custom slides with all unique HTML as follows.
```html
<slider class="app">
    <template v-slot:slides="props">
        <slide :style="{ 'background-image': `url('img-src/${props.code}/theme/slide-1.jpg')` }">
            <p>Slide 1</p>
        </slide>
        <slide :style="{ 'background-image': `url('img-src/${props.code}/theme/slide-2.jpg')` }">
            <p>Slide 2</p>
        </slide>
        <slide :style="{ 'background-image': `url('img-src/${props.code}/theme/slide-3.jpg')` }">
            <p>Slide 3</p>
        </slide>
        <slide :style="{ 'background-image': `url('img-src/${props.code}/theme/slide-4.jpg')` }">
            <p>Slide 4</p>
        </slide>
        <slide :style="{ 'background-image': `url('img-src/${props.code}/theme/slide-5.jpg')` }">
            <p>Slide 5</p>
        </slide>
    </template>
</slider>
```

<a name="custom-slides-loop"></a>
## Custom Slides Loop
You can create custom slides and loop through the images using the example tomorrow.
```html
<slider class="app" number-of-images="5">
    <template v-slot:slides="props">
        <slide v-for="slide in props.slides"
               :style="{ 'background-image': `url('img-src/${props.code}/theme/${slide}')` }">
            <p>{{ slide }}</p>
        </slide>
    </template>
</slider>
```

<a name="custom-slides-endpoint"></a>
## Custom Slides with Endpoint
The above custom slides can also be used when using an endpoint.
```html
<slider class="app" endpoint="/api/v1/vehicle-slider" vehicle-id="{DETAIL_ID}">
    <template v-slot:slides="props">
        <slide v-for="slide in props.slides" :style="{ 'background-image': `url('${slide}')` }">
            <p>{{ slide }}</p>
        </slide>
    </template>
</slider>
```
