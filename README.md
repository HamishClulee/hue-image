# hue-image

Leverage IntersectionObserver API to provide lazy-loading and smart responsive behavior by default for &lt;img> tags

Intended as a convenience component for images in the vue eco-system, (ie11+ will require a polyfill, or use my other repo, hue-image-ie).

This component is built with responsiveness and performance in mind. Lazy load all images, and don't request large image sizes for small screens.

Intended to be used by copying and modifying the source file, not intended to be used as a dependency.

## What It Does

This component ensures that any images contained within a view are only requested from the server when scrolled into the viewport (by default), or are loaded at a configutable point X pixels before being scrolled into the viewport.

It provides a placeholder SVG so the page doesn't jump around as images are requested, loaded and painted. Currently the placeholder is just an SVG image with base64 encoding.

Provides the ability to provide a value to the images `srcset` attribute, via the prop `srcmap`, the documentation for `srcset` can be found (here)[https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#Attributes]

The format of the `srcmap` prop attempts to simplify the `<img>` `srcset` attribute an example of the prop value follows:
```
this.srcmap = {
    'small': 'path/to/small/image', // for screen widths below 480px
    'medium': 'path/to/medium/image', // for screen widths between 481px and 1280px
    'large': 'path/to/large/image', // for screen widths larger than 1281px
}
```

It would be easy to provide support for changing the breakpoints in the the example above, if thats something you need.