<!-- Space: ~213834277 -->
<!-- Parent: Web Documentation -->
<!-- Parent: Vue Components -->
<!-- Title: Finance Calculator -->
<!-- Layout: (plain) -->

# Finance Calculator

Many basic settings can be modified using the settings page within web planner. Also attempt to make the changes here before adding custom templates.

This component has got slots which you can modify, you simply add the following between the component name:

```html
<template v-slot:slotName="slotProps">
    <!-- Content Here -->
</template>
```

Slot name should be replaced with the name of the slot, of course. These can be found within the settings if you toggle on display slots, however here is a list:

- loading
- header
- deposit
- deposit-label
- deposit-value
- deposit-input
- term
- term-label
- term-value
- term-input
- mileage
- mileage-label
- mileage-value
- mileage-input
- quote
- quote-type
- quote-example
- quote-table
- quote-applyy-button
- quote-print-button
- adjustment-message

So let's say I want to change, so it's within a `h1` rather than `h2`.

```html
<finance-calculator class="app" vehicle-id="1815981">
    <template v-slot:header="slotProps">
        <header :class="{ slot: slotProps.data.showSlots }" data-slot="header">
            <h1>{\{ slotProps.data.header }\}</h1>
            <p>{\{ slotProps.data.subtitle }\}</p>
        </header>
    </template>
</finance-calculator>
```

`slotProps.data` contains all the data avaliable to you, from the component, to look in here you can just dump it out like so:
```html
<finance-calculator class="app" vehicle-id="1815981">
    <template v-slot:header="slotProps">
         {\{ slotProps.data.header }\}
    </template>
</finance-calculator>
```

> {note} If your copying and pasting code above from here ensure to remove the `\` from between the `{{` and `}}`, due to the documentation using `Vue` these had to be escaped.

Below is a list of the default settings, so you can see what you can use within the slots:

```javascript
{
    initialized: false,
    loading: true,
    deposit_adjustment: false,
    has_adjustments: false,
    error: null,
    quotes: [],
    video: null,
    mousedown: false,
    videoUrls: {
        HP: 'https://www.youtube.com/embed/_gAT2C1RBeo',
        PCP: 'https://www.youtube.com/embed/HVjpC6weQdI'
    },
    selected: null,
    deposit_range: [ 500, 20000 ],
    deposit_steps: 500,
    mileage_range: [ 8000, 30000 ],
    mileage_steps: 1000,
    finance_example_toggles: {
        'HP': false,
        'PCP': false,
        'CS': false,
    },
    deposit_marks_enabled: false,
    term_marks_enabled: true,
    mileage_marks_enabled: false,

    deposit: 500,
    mileage: 10000,
    term: 60,
    term_options: [ 6, 12, 18, 24, 30, 36, 42, 48, 54, 60 ],

    header: 'Finance Options',
    subtitle: 'Our finance partners offer competitive quotes for all circumstances.',
    show_representative_examples: true,
    show_print_button: true,
    show_apply_button: true,
    sliders_tooltip: 'focus',
    dark_mode: false,

    hide_deposit_adjustment: false,
    hide_term_adjustment: false,
    hide_mileage_adjustment: false,
}
```

<a name="styles"></a>
## Styles
```scss
@import '~vue-slider-component/lib/theme/default.scss';

    @mixin for-phone-only {
        @media (max-width: 739px) { @content; }
    }

    $accent-colour: rgb(255, 121, 0);
    $primary-colour: rgb(33, 86, 160);
    $apply-colour: rgb(43, 159, 87);

    $borderColor: rgba(0,0,0,.1);
    $tableColor: rgba(0,0,0,.04);
    $borderHover: rgba(0,0,0,.2);
    $textColour: #111;
    $tooltipBackground: $primary-colour;
    $tooltipColour: #fff;
    $opaqueColour: rgba(255,255,255,.8);
    $textColourSubtle: #777;

    $darkBorderColor: rgba(255, 255, 255, 0.1);
    $darkTableColor: rgba(255,255,255,.1);
    $darkBorderHover: rgba(255, 255, 255, 0.2);
    $darkTextColour: #fff;
    $darkTooltipBackground: $primary-colour;
    $darkTooltipColour: #fff;
    $darkOpaqueColour: rgba(0,0,0,.8);
    $darkTextColourSubtle: rgba(255,255,255,.6);

    .finance-calculator {
        font-family: Roboto, Trebuchet, Arial, sans-serif;
        color: $textColour;
        header {
            font-family: inherit;
            background: $borderColor;
            padding: 20px;
            text-align: center;
            border: 1px solid $borderColor;
            font-weight: bold;
            p, h1, h2, h3, h4 h5 {
                color: $textColour;
            }
        }
        .sliders {
            display: flex;
            justify-content: center;
            align-items: center;
            border-width: 0 1px 0 1px;
            border-color: $borderColor;
            border-style: solid;
            padding: 10px;
            height: 110px;
            @include for-phone-only {
                display: block;
                height: auto;
                .agreement {
                    height: 75px;
                }
            }
            & > div {
                @include for-phone-only {
                    margin: 20px 0;
                }
                flex-grow: 1;
                padding: 0 10px;
                .label, .value {
                    width: calc(50% - 10px);
                    display: inline-block;
                    text-transform: uppercase;
                    letter-spacing: .05em;
                    font-size: 11px;
                    color: $textColour;
                    line-height: 11px;
                    font-weight: 400;
                }
                .value {
                    text-align: right;
                }
            }
        }
        .quotes {
            display: flex;
            padding: 10px;
            border: 1px solid $borderColor;
            @include for-phone-only {
                display: block;
            }
            & > div {
                flex-grow: 1;
                border: 4px solid $borderColor;
                border-radius: 4px;
                margin: 5px;
                position: relative;
                transition: border .2s ease-in-out;
                will-change: border;
                &:hover {
                    border: 4px solid $borderHover;
                    p.type {
                        background: $borderHover;
                    }
                }
                &:after {
                    content: 'Loading...';
                    position: absolute;
                    top: 0;
                    left: 0;
                    width: 100%;
                    height: 100%;
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    background: $opaqueColour;
                    font-size: 22px;
                    pointer-events: none;
                    opacity: 0;
                    transition: opacity .2s ease-in-out;
                    will-change: opacity;
                }
                &.loading {
                    pointer-events: none;
                    &:after {
                        opacity: 1;
                    }
                }
                p.type {
                    background: $borderColor;
                    line-height: 44px;
                    padding: 0 20px;
                    font-size: 15px;
                    color: $textColour;
                    transition: background .2s ease-in-out;
                    will-change: background;
                }
                p.title {
                    font-size: 16px;
                    font-weight: 700;
                    color: $textColour;
                    text-align: left;
                    padding: 0 10px;
                }
                .payments {
                    font-weight: 800;
                    padding: 0 10px;
                    font-size: 12px;
                    font-family: inherit;
                    color: #000;
                    td:last-child {
                        text-align: right;
                        padding-right: 0;
                        span {
                            background: $accent-colour;
                            color: #fff;
                            padding: 13px;
                            font-family: inherit;
                        }
                    }
                }
                .ci-play-circle {
                    cursor: pointer;
                    margin-right: 5px;
                    color: $primary-colour;
                }
                table {
                    width: calc(100% - 20px);
                    margin-left: 10px;
                    background: none;
                    tr td {
                        line-height: 40px;
                        border: none;
                        background: none;
                        color: $textColourSubtle;
                        font-weight: 700;
                        text-align: left;
                        padding: 0 10px;
                        &:last-child {
                            color: #000;
                            text-align: right;
                        }
                        span.adjusted {
                            color: rgb(214, 53, 53);
                            &:after {
                                content: ' *';
                            }
                        }
                    }
                    tr:nth-child(odd) td {
                        background: $tableColor;
                    }
                }
            }
            .cta {
                padding: 20px;
                display: flex;
                justify-content: center;
                align-items: center;
                a {
                    color: #fff;
                    background: rgb(48, 63, 92);
                    padding: 10px;
                    border-radius: 3px;
                    text-decoration: none;
                    text-transform: uppercase;
                    font-size: 12px;
                    margin: 0 10px;
                    position: relative;
                    i {
                        margin-left: 10px;
                    }
                    &:after {
                        content: '';
                        position: absolute;
                        top: 0;
                        left: 0;
                        width: 100%;
                        height: 100%;
                        background-color: rgba(255,255,255,.2);
                        transition: .2s ease-in-out;
                        opacity: 0;
                    }
                    &:hover:after {
                        opacity: 1;
                    }
                }
                a.apply { background: $apply-colour; }
                a.print { background: $primary-colour; }
            }
        }
        .adjustment {
            text-align: center;
            margin-top: 10px;
            font-size: 12px;
        }

        .vue-slider:hover .vue-slider-rail { background-color: #ccc; }
        .vue-slider-rail { background-color: #ccc; }
        .vue-slider-process { background-color: $primary-colour; }
        .vue-slider-dot {
            width: 20px !important;
            height: 20px !important;
            border-radius: 50%;
            background-color: $primary-colour;
            cursor: move;
            &-handle {
                width: 8px;
                height: 8px;
                position: absolute;
                top: 6px;
                left: 6px;
                cursor: move;
            }
        }
        .vue-slider-mark-label {
            font-size: 11px;
        }
        .vue-slider-dot-tooltip-inner {
            .vue-slider-dot-tooltip-text {
                color: $tooltipColour;
            }
            border-color: $tooltipBackground;
            background-color: $tooltipBackground;
        }

        /** Dark Mode Theme **/
        &.dark {
            * {
                color: $darkTextColour;
            }
            header {
                background: $darkBorderColor;
                border: 1px solid $darkBorderColor;
                p, h1, h2, h3, h4 h5 {
                    color: $darkTextColour;
                }
            }
            .sliders {
                border-color: $darkBorderColor;
                & > div .label, .value {
                    color: $darkTextColour;
                }
            }
            .quotes {
                border: 1px solid $darkBorderColor;
                & > div {
                    border: 4px solid $darkBorderColor;
                    &:after { background: $darkOpaqueColour; }
                    &:hover {
                        border: 4px solid $darkBorderHover;
                        p.type {
                            background: $darkBorderHover;
                        }
                    }
                    p.type {
                        background: $darkBorderColor;
                        color: $darkTextColour;
                    }
                    p.title {
                        color: $darkTextColour;
                    }
                    .payments {
                        color: #000;
                        td:last-child span {
                            color: #fff;
                        }
                    }
                    table {
                        tr td {
                            color: $darkTextColourSubtle;
                            &:last-child {
                                color: $darkTextColour;
                            }
                            span.adjusted {
                                color: rgb(214, 53, 53);
                            }
                        }
                        tr:nth-child(odd) td {
                            background: $tableColor;
                        }
                    }
                }
            }
            .vue-slider-dot-tooltip-inner {
                .vue-slider-dot-tooltip-text {
                    color: $darkTooltipColour;
                }
                border-color: $darkTooltipBackground;
                background-color: $darkTooltipBackground;
            }
        }
    }

    .slot {
        position: relative;
        &:before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border: hsl(348, 100%, 61%) dashed 1px;
            transition: all .2s ease-in-out;
            background: transparent;
        }
        &:hover:before {
            background: rgba(255, 56, 96, .2);
        }
    }

    .slide-up-enter-active, .slide-up-leave-active {
        transition: all .5s;
    }
    .slide-up-enter, .slide-up-leave-to {
        opacity: 0;
        transform: translateY(100px);
    }
```
