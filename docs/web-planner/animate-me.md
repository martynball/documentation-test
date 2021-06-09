<!-- Space: WE -->
<!-- Parent: Web Documentation -->
<!-- Parent: Web Planner -->
<!-- Title: Animate-me -->
<!-- Layout: (plain) -->

# Animate-me

This script will allow you to easily add a class to row-block / top level element as they come into the viewport to trigger any animations you want on the elements contained.

## Useage

Add a class of '.animate-me' to the row-block / top level element containing the elements you wish to animate into view.

## Example HTML
```
<div class="row-block example-panel animate-me">
    <h1>Example</h1>
</div>
```

## Example Less

Below is some example less for applying your styles/animations to the elements

```
// All your styles / animations will be within the top level element less
.row-block.example-panel {
    // Set your starting state for animation e.g
    h1 {
        opacity: 0;
        transition: all 0.2s linear;
    }

    // Add a nested class of ani-active within the row-block / panel less
    &.ani-active {
        // Set your finishing state for animation e.g
        h1 {
            opacity: 1;
            transition: all 0.2s linear;
        }
    }
}
```
