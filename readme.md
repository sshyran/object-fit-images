100% untested at the moment. Will test soon

# object-fit-images [![module size](https://badge-size.herokuapp.com/bfred-it/object-fit-images/master/ofi.min.js) ![module gzipped size](https://badge-size.herokuapp.com/bfred-it/object-fit-images/master/ofi.min.js?compression=gzip)](https://github.com/bfred-it/object-fit-images/blob/master/ofi.min.js)

> Adds support to `object-fit` to images on IE9, IE10, IE11 and Edge

This script was made with the main use-case in mind: images on IE/Edge. Main features:

- The code is light on the CPU
- No other elements are created to make it work
- Once set, position is taken care by the browser
- You can normally get and set the `<img>`'s `src` attribute: `img.src = 'other-image.jpg'`

## Comparison table with alternative solutions

Support                           | object-fit-images _(this)_                                     | [tonipinel/object-fit-polyfill](https://github.com/tonipinel/object-fit-polyfill)           | [jonathantneal/fitie](https://github.com/jonathantneal/fitie)
:---                              | :---                                                           | :---                                                                                        | :---
Browsers                          | IE 9-11, Edge                                                  | "All browsers"                                                                              | IE 8-11, Edge
Tags                              | `img`                                                          | `img`                                                                                       | `img`, `video`
`cover/contain`                   | 💚                                                              | 💚                                                                                           | 💚
`fill`                            | 💚                                                              | 💚                                                                                           | 💚
`none`                            | 💚                                                              | 💚                                                                                           | 💔
`scale-down`                      | 💔                                                              | 💔                                                                                           | 💔
`object-position`                 | 💚                                                              | 💔                                                                                           | 💔

Performance                       | object-fit-images _(this)_                                     | [tonipinel/object-fit-polyfill](https://github.com/tonipinel/object-fit-polyfill)           | [jonathantneal/fitie](https://github.com/jonathantneal/fitie)
:---                              | :---                                                           | :---                                                                                        | :---
Size                              | 1.2KB                                                          | 1.8KB                                                                                       | 1.5KB
Update wait                       | 💚 No wait, applied before image load                           | 💚 No wait, applied before image load                                                        | 💔 Wait until full image load
Additional DOM elements necessary | 💚 No                                                           | 💔 Yes, a wrapping element is added                                                          | 💔 Yes, a wrapping element is added
Performance overhead              | 💰                                                              | 💰💰💰                                                                                         | 💰💰
Technique description             | Transparent `src` image; Image in `<img>`'s `background`       | Wrapper element with style copied from `<img>`; CSS+JS positioning; Original `<img>` hidden | Wrapper element with style copied from `<img>`; JS positioning

Ease of use                       | object-fit-images _(this)_                                     | [tonipinel/object-fit-polyfill](https://github.com/tonipinel/object-fit-polyfill)           | [jonathantneal/fitie](https://github.com/jonathantneal/fitie)
:---                              | :---                                                           | :---                                                                                        | :---
Object-fit definition             | 💚 Automatic in CSS                                             | 💔 Via `data` attribute in HTML (`data-object-fit="cover"`)                                  | 💔 Via class in HTML (`class="cover"`)
Updates on resize                 | 💚 Unnecessary if media queries don't change `object-fit`       | 💛 Unnecessary if media queries don't change `object-fit`, impossible otherwise.             | 💔 Yes, manually
Updates on `object-fit` change    | 💚 Automatic                                                    | 💔 Impossible                                                                                | 💔 Impossible
Fix new elements automatically    | 💚 Optional                                                     | 💔 Impossible                                                                                | 💛 Manually
`<img>` `src` changes             | 💚 Automatically reflected                                      | 💔 Image not updated at all                                                                  | 💔 Fix not updated
Other limitations                 | 💔 Any `onload` events on `<img>` will fire again when it fixes | 💚 I didn't find any                                                                         | 💔 Some CSS declaration might be broken because partially moved to the wrapper


Runner-up: [anselmh/object-fit](https://github.com/anselmh/object-fit) is deprecated, doesn't support Edge and clocks in at 14KB.

## Usage

Fix all the images on the page, present and future.

```js
objectFitImages();
```

Alternatively, just fix them once. The first parameter can be:

```js
// a selector
objectFitImages('img.some-image');

// an array/NodeList
var someImages = document.querySelectorAll('img.some-image');
objectFitImages(someImages);

// a single element
var oneImage = document.querySelector('img.some-image');
objectFitImages(oneImage);
```

You can safely disable the `resize` listener this way:

```js
objectFitImages('img.some-image', {onresize: false});
```

... if your code DOESN'T contain something like this:
```css
                            img { object-fit: cover }
@media (max-width: 500px) { img { object-fit: contain } }
```

## Load and enable with plain HTML

```html
<script src="ofi.min.js"></script>
<script>objectFitImages();</script>
```

## Load with with browserify

```sh
npm install --save object-fit-images
```

```js
var objectFitImages = require('object-fit-images');
objectFitImages();
```

## API

### `objectFitImages([images, [opts]])`

parameter                         | description
---                               | ---
**`images`**                      | Type: `string` (as a selector) or `array`-like *optional* <br> The images to apply the fix on. If it's not supplied, OFI will enter the automatic mode (which means that new images in the DOM will automatically be fixed).
**`opts`**                        | Type: `object` *optional* <br> Set to `{onresize: false}` if you don't expect `object-fit` to vary in a media query.


## License

MIT © [Federico Brigante](http://twitter.com/bfred_it)
