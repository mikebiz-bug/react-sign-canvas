
### Props

The props of SignatureCanvas mainly control the properties of the pen stroke used in drawing.
All props are **optional**.

- `velocityFilterWeight` : `number`, default: `0.7`
- `minWidth` : `number`, default: `0.5`
- `maxWidth` : `number`, default: `2.5`
- `minDistance`: `number`, default: `5`
- `dotSize` : `number` or `function`,
  default: `() => (this.minWidth + this.maxWidth) / 2`
- `penColor` : `string`, default: `'black'`
- `throttle`: `number`, default: `16`

There are also two callbacks that will be called when a stroke ends and one begins, respectively.

- `onEnd` : `function`
- `onBegin` : `function`

Additional props are used to control the canvas element.

- `canvasProps`: `object`
  - directly passed to the underlying `<canvas />` element
- `backgroundColor` : `string`, default: `'rgba(0,0,0,0)'`
  - used in the [API's](#api) `clear` convenience method (which itself is called internally during resizes)
- `clearOnResize`: `bool`, default: `true`
  - whether or not the canvas should be cleared when the window resizes

Of these props, all, except for `canvasProps` and `clearOnResize`, are passed through to `signature_pad` as its [options](https://github.com/szimek/signature_pad#options).
`signature_pad`'s internal state is automatically kept in sync with prop updates for you (via a `componentDidUpdate` hook).

### API

All API methods require a ref to the SignatureCanvas in order to use and are instance methods of the ref.

```javascript
<SignatureCanvas ref={(ref) => { this.sigCanvas = ref }} />
```

- `isEmpty()` : `boolean`, self-explanatory
- `clear()` : `void`, clears the canvas using the `backgroundColor` prop
- `fromDataURL(base64String, options)` : `void`, writes a base64 image to canvas
- `toDataURL(mimetype, encoderOptions)`: `base64string`, returns the signature image as a data URL
- `fromData(pointGroupArray)`: `void`, draws signature image from an array of point groups
- `toData()`: `pointGroupArray`, returns signature image as an array of point groups
- `off()`: `void`, unbinds all event handlers
- `on()`: `void`, rebinds all event handlers
- `getCanvas()`: `canvas`, returns the underlying canvas ref.
  Allows you to modify the canvas however you want or call methods such as `toDataURL()`
- `getTrimmedCanvas()`: `canvas`, creates a copy of the canvas and returns a [trimmed version](https://github.com/agilgur5/trim-canvas) of it, with all whitespace removed.
- `getSignaturePad()`: `SignaturePad`, returns the underlying SignaturePad reference.

The API methods are _mostly_ just wrappers around [`signature_pad`'s API](https://github.com/szimek/signature_pad#api).
`on()` and `off()` will, in addition, bind/unbind the window resize event handler.
`getCanvas()`, `getTrimmedCanvas()`, and `getSignaturePad()` are new.

## Example

You can interact with the example in a few different ways:

1. Run `npm start` and navigate to [http://localhost:1234/](http://localhost:1234/).<br>
Hosted locally via the [`example/`](example/) directory
1. [View the live demo here](https://agilgur5.github.io/react-signature-canvas/).<br>
Hosted via the [`gh-pages` branch](https://github.com/agilgur5/react-signature-canvas/tree/gh-pages), a standalone version of the code in [`example/`](example/)
1. [Play with the CodeSandbox here](https://codesandbox.io/s/github/agilgur5/react-signature-canvas/tree/cra-example).<br>
Hosted via the [`cra-example` branch](https://github.com/agilgur5/react-signature-canvas/tree/gh-pages), a standalone version using [Create React App](https://github.com/facebook/create-react-app).
