<!-- Space: ~213834277 -->
<!-- Parent: Web Documentation -->
<!-- Parent: Vue Components -->
<!-- Title: Video Frame -->
<!-- Layout: (plain) -->

# Video Frame

This is a **Vue** component, so Vue must be enabled on your website for this to work. Use this to lazy load iframes into your website.

Technically any **iframe** will work even though this was meant for videos, such as youtube.

<a name="example"></a>
## Example Usage
```html
<video-frame class="flexible-frame app" path="https://www.youtube.com/embed/aC87_RCAxog?autoplay=1" provider="youtube"></video-frame>
```

| Setting | Type | Example |
| ------- | ---- | ------- |
| placeholder | Array/String | `[ [ 'img-src/{v2_FOLDER}/theme/placeholder.jpg', 128 ] ]` or `/img-src/{v2_FOLDER}/theme/placeholder.jpg` |
|<td colspan=3>The placeholder can be used 2 ways, either pass in a single image, or pass in an array which will be used as the srcset. You must format the array correctly however, this is for more advanced users.
| placeholder-srcset | Boolean | false |
| <td colspan=3>Only use this if the placeholder is a string, by enabling this the component will create a srcset from the image you provide, it will append a number onto your placeholder so please ensure you create these images within your theme folder, example based on the above placeholder: `/img-src/{v2_FOLDER}/theme/placeholder-120w.jpg` |
| path | String | https://www.youtube.com/embed/aC87_RCAxog?autoplay=1 |a
| <td colspan=3> This is simply the url to the iFrame, as stated above any link can be used, just ensure you provide a placeholder. |
| provider | String | youtube
| <td colspan=3>It is recommended that you provide the provider, so for a youtube embed link the provider would be youtube. If you don't provide this the component will try and get it from the URL, but this is not recommended. |
| play-icon | String | fa fa-play |
| <td colspan=3> Use this to over-ride the play icon which is used. |
| load-icon | String | ci ci-spinner-l |
| <td colspan=3> Use this to over-ride the loading icon which is used. |
| instant-hide | Boolean | false |
| <td colspan=3> When the play button the iFrame is loaded, once loaded the placeholder image and loading icon is removed, change this value to true to remove the placeholder and icon instantly without waiting for the iFrame to load. |
| provider-logo | Boolean | false |
| <td colspan=3> Not fully finished, this will simply add the provider's logo to the top left of the placeholder, however this expects the font-awesome logo to be named as follows: fa fa-provider. |

> {note} Please note, if you use a setting above which does not have a type of String, then you must add `:` before the setting, for example `:placeholder-srcset="true"`

<a name="default-component"></a>
## Default Component HTML
Below is the default HTML, if you wish to over-ride any of this then you must please all of the below code between the video-frame tags.

```html
<div class="video-frame">
    <div class="video-frame__overlay" v-if="displayOverlay" @click="toggled = true">
        <div class="video-frame__overlay--logo" v-if="logoEnabled">
            <i :class="logo"></i>
        </div>
        <div class="video-frame__overlay--icon">
            <i :class="'play ' + playIcon" v-if="!toggled"></i>
            <i :class="'load ' + loadIcon" v-if="toggled"></i>
        </div>
        <div class="video-frame__overlay--image">
            <img :src="src" :srcset="srcset" alt="">
        </div>
    </div>
    <iframe class="video-frame__iframe"
            v-if="toggled"
            v-show="displayed"
            :src="path"
            @load="displayed = true"
            frameborder="0"
            allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen></iframe>
</div>
```

<a name="default-less"></a>
## Default Component LESS

```css
.video-frame {
    overflow: hidden;
    &__overlay {
        height: 100%;
        width: 100%;
        position: absolute;
        &--logo {
            position: absolute;
            top: 0;
            left: 0;
            font-size: 40px;
            color: #fff;
            z-index: 9;
            padding: 0 10px;
        }
        &--icon {
            left: 0;
            position: absolute;
            top: 0;
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 9;
            i {
                font-size: 5vw;
                color: #fff;
                &.load {
                    @keyframes spin {
                        0% {
                            transform: rotate(0deg);
                        }
                        100% {
                            transform: rotate(360deg);
                        }
                    }
                    animation: spin 2s infinite linear;
                }
                &.play {
                    cursor: pointer;
                    transition: all .2s ease-in-out;
                    &:hover {
                        transform: scale(1.3);
                    }
                }
            }
        }
        &--image, &--image img {
            width: 100%;
            height: 100%;
        }
        &--image:before {
            content: '';
            position: absolute;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,.5);
        }
    }
    &__iframe { }
}
```
