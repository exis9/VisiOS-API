# VisiOS API Documentation

As of the version 1.1.3, VisiOS will be introducing the VisiAPI.

(Sorry, I've been writing this doc and it's still a draft. Not ready yet! ^^)

## fetch
Fetch from the target URL
```js
// This will fetch the html of the target URL
async function test(){
	let text = await VisiAPI('fetch', {url:'https://google.com'})
	console.log( text )
}
test()

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

// for example, if you have a folder named "My Documents" on the desktop 3
VisiAPI('openFile', {idx:3, path:'My Documents'})

// If you also want to specify the size (This works only for folders)
VisiAPI('openFile', {idx:3, path:'My Documents', w:700, h:400}) //Specify the width and height
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

// Specify the size and starting coordinates
VisiAPI('open', {url:'https://url_to_open', w:700, h:500, x:100, y:10})

// HTML
VisiAPI('open', {html:'<h1>Hello!</h1><br><br>This is HTML!'})

// HTML + JS
VisiAPI('open', {html:'<h1>Hello!</h1><br><br>This is HTML!', script:'alert("Wow!")'})
```


# Storage APIs

## localStorage_get
If you pass a key name, this will return the key's value from the local storage, or null if the key does not exist

```js
async function test(){
	VisiAPI('localStorage_set', {n:'test_key', v:'Wow VisiOS!!'})
	let v = await VisiAPI('localStorage_get', {n:'test_key'})
	alert( v ) //wow!!
}
test()
```

## localStorage_set
If you pass a key name and value, this will add that key to the local storage, or update that key's value if it already exists.

```js
VisiAPI('localStorage_set', {n:'test_key', v:'Wow!!'})
```

## memStorage_get
If you pass a key name, this will return the key's value from the memory storage, or null if the key does not exist.
The memory storage is shared among all the VisiOS apps and is cleared when the user closes the tab.
This feature is good for storing temporary data that you want to share among multiple apps in real-time.

```js
async function test(){
	VisiAPI('memStorage_set', {n:'test_key', v:'Wow VisiOS!!'})
	let v = await VisiAPI('memStorage_get', {n:'test_key'})
	alert( v ) //wow!!
}
test()
```

## memStorage_set
If you pass a key name and value, this will add that key to the memory storage, or update that key's value if it already exists.
The memory storage is shared among all the VisiOS apps and is cleared when the user closes the tab.

```js
VisiAPI('memStorage_set', {n:'test_key', v:'Wow!!'})
```
