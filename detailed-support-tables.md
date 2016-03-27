# Detailed support of object-fit-images

> OFI in short

OFI is meant to add support of `object-fit` and `object-position` to **IEdge 9-13, Android 4.4-**, but I might edit it to add `object-position` support to **Safari OSX/iOS**

## Responsive images support

### `object-fit-images` + `srcset` 

💚 Supported in the browsers above, with [`picturefill`](https://github.com/scottjehl/picturefill) where necessary, but:

* 💔 In Edge 12, OFI picks the `src` attribute instead of what's in `srcset` because `currentSrc`. I need to look into forcing `picturefill` to override the native `srcset` support
* 💛 If I add Safari support for `object-position` to OFI, Safari might suffer of the above issue

### `object-fit-images` + `picture`

💚 Supported in the browsers above, with [`picturefill`](https://github.com/scottjehl/picturefill) where necessary, but:

* 💔 Edge 13+ overrides OFI's fix with what's in `<source>` (maybe I can fix it by removing `<source>` tags but then it'd lose responsiveness). I need to look into forcing `picturefill` to override the native `picture` support
* 💛 If I add Safari support for `object-position` to OFI, Safari might suffer of the above issue

## Can I Use

* [`object-fit`](http://caniuse.com/#feat=object-fit)
* [`srcset`](http://caniuse.com/#feat=srcset)
* [`picture`](http://caniuse.com/#feat=picture)
