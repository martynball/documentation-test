<!-- Space: ~213834277 -->
<!-- Parent: Web Documentation -->
<!-- Parent: Vue Components -->
<!-- Title: Credit Calculator Slider -->
<!-- Layout: (plain) -->

# Credit Calculator Slider

This component will send a request to iVendi for a quote based on the amount you want to borrow, and the duration.

```html
<credit-calculator-sliders class="app"></credit-calculator-sliders>
```

```html
<credit-calculator-summary class="app"></credit-calculator-summary>
```

<a name="legacy-props"></a>
## Legacy Props
Props will always over-ride defaults and settings from planner.

| Setting| Type | Default | 
|-------- | ---- | ------- |
| borrow-step | Number | 500 | 
| min-borrow | Number |  2000 |
| ma-borrow | Number | 40000 |
| default-borrow | Number | 10000 |
| term-step | Number | 12 |
| min-term | Number| 12 |
| max-term | Number | 60 |
| default-term | Number | 60 |

<a name="credit-calculator-summary"></a>
## Credit Calculator Summary
| Prop| Type | Default | 
|-------- | ---- | ------- |
|deposit-percentage | Number | 10|
|offset | Number | 0 |
|finance-button | String | Free Finance Check |

All the prop can be used to override the default value

<a name="example-useage"></a>
## Example Usage with Prop

```html
<credit-calculator-sliders class="app" :borrow-step="1000"></credit-calculator-sliders>
```

This will override the step each time you move the slider by 1000.
However sometimes it Vue varies to use the prop. It will be either with colon or without

<a name="change-log"></a>
## Changelog
### 17/11/2020 (Development Notes - Not Live)
- Separated current component into a theme, base component will now lazy load in the current version if that theme is selected, allow us to add more themes and their own logic. This has been done so that iVendi's other endpoint can be used to allow CreditTiers to be introduced. Also means any dealers wanting to switch the CreditTiers don't need templates or page text updating, as old version will work in-line with new one without braking, retained props for older versions.
- Due to the CreditTiers requesting data directly from them rather than us Curl'ing from our endpoint, I have done the same logic for our current Finance Calculator. So now the quote doesn't run through `quoteware3`, all this did was build up a request, this logic is done within the component. We only require the `Username` and `QuoteeUID` from the dealer record which is brought in with the settings.
- Moved the request logic to the sliders component, the summary component now just displays the data, there is no other logic within this component.
- Retained all the previous props on the sliders component for legacy uses, the props will over-ride the defaults or anything set within the settings table.
- Couldn't retain the `depositPercentage` or `financeButton` prop from the summary component, provide unreliable and clumberson to send this to the sliders component, as now this logic is performed here. Will need to do a global search to ensure no dealers are using these 2 props, unlikley.
- Clicking `See my payments` will now wait for a quote response before scrolling, to avoid scrolling to nothing.
- Multiple requests made during sliding of slider will now be cancelled, better option would be to de-bounce the request, so a request is only made when stopped sliding, but this will be fine for now. 
