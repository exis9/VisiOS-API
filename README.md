# VisiOS API Documentation

As of the version 1.1.3, VisiOS will be introducing the VisiAPI.

(Sorry, I've been writing this doc and it's still a manifest. Not ready yet! ^^)

## fetch
Fetch from the target URL
```js
// This will fetch the html of the target URL
let text = VisiAPI('fetch', {url:'https://url...'}) 
console.log( text )

// NOTE: ↓ You can also specify "options" just like the JavaScript fetch
// https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch
VisiAPI('fetch', {url:'https://url...', options: {mode:..., method:..., body:... }}) 
```

## copyToClipboard
Copy text to the clipboard
```js
VisiAPI('copyToClipboard', {text:'Text to copy'}) 
```

## openFile
Open the file path you specified
```js
// ↓ You can open folders or files by setting the desktop index number(1-9) and file path to a folder or a file.
VisiAPI('openFile', {idx:1, path:'file_path_to_open'})
```
## close
Close the current app
```js
VisiAPI('close')
```
## open
Open URL(or execute HTML/JavaScript) in a new VisiOS window
```js
// Open URL
VisiAPI('open', {url:'https://url_to_open'})

// HTML
VisiAPI('open', {html:'<h1>Hello!</h1><br><br>This is HTML!'})

// HTML + JS
VisiAPI('open', {html:'<h1>Hello!</h1><br><br>This is HTML!', script:'alert("Wow!")'})
```

