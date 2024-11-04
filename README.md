# VisiOS API Documentation

As of the version 1.1.3, VisiOS will be introducing the VisiAPI.

## fetch
```js
// This will fetch the html of the target URL
let text = VisiAPI('fetch', {url:'https://url...'}) 
console.log( text )

// NOTE: ↓ You can also specify "options" just like the JavaScript fetch
// https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch
VisiAPI('fetch', {url:'https://url...', options: {mode:..., method:..., body:... }}) 
```

## copyToClipboard
```js
VisiAPI('copyToClipboard', {text:'Text to copy'}) 
```
