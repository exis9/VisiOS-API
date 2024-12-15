# VisiOS API Documentation

As of the version 1.1.4, VisiOS has introduced the VisiAPI.

(Sorry, I've been writing this doc and it's still a draft. Not perfectly ready yet! ^^)

# Index

🟩 [General APIs](#fetch)<br>
　🔷 [ver](#ver)<br>
　🔷 [fetch](#fetch)<br>
　🔷 [copyToClipboard](#copytoclipboard)<br>

🟩 [File APIs](#file-apis)<br>
　🔷 [openFile](#openfile)<br>
　🔷 [openPage](#openPage)<br>
　🔷 [closeWindow](#closeWindow)<br>

🟩 [Storage APIs](#storage-apis)<br>
　🔷 [localStorage_set](#localstorage_set)<br>
　🔷 [localStorage_get](#localstorage_get)<br>
　🔷 [memStorage_set](#memstorage_set)<br>
　🔷 [memStorage_get](#memstorage_get)<br>
　🔷 [appStorage_set](#appstorage_set)<br>
　🔷 [appStorage_get](#appstorage_get)<br>

---

<div id="user-content-toc">
	<ul align="center" style="list-style: none;">
		<summary>
			<h1>General APIs</h1>
		</summary>
	</ul>
</div>

## ver
Get the current VisiOS version number
```js
async function showVersion(){
	let text = await VisiAPI('ver')
	alert( text )
}
showVersion()
```

## fetch
Fetch from the target URL
```js
// This will fetch the html of the target URL
async function test(){
	let text = await VisiAPI('fetch', {url:'https://google.com'})
	alert( text ) //display the html of the target URL
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

---

<div id="user-content-toc">
	<ul align="center" style="list-style: none;">
		<summary>
			<h1>File APIs</h1>
		</summary>
	</ul>
</div>

## openFile
Open the file path you specified
```js
// ↓ You can open folders or files by setting the desktop index number(1-9) and file path to a folder or a file.
VisiAPI('openFile', {desktopId:1, path:'file_path_to_open'})

// for example, if you have a folder named "My Documents" on the desktop 3
VisiAPI('openFile', {desktopId:3, path:'My Documents'})

// If you also want to specify the size (This works only for folders)
VisiAPI('openFile', {desktopId:3, path:'My Documents', w:700, h:400}) //Specify the width and height
```
```js
// If you have a bookmark named Google on the desktop 1, you can open the bookmark like these:
VisiAPI('openFile', {path:'Google', x:10, y:10, w:700, h:400}) //open in new VisiOS window (NOTE: x, y, w, h are optional)
VisiAPI('openFile', {path:'Google', type:'newTab'}) //open in new tab
VisiAPI('openFile', {path:'Google', type:'newWindow', x:0, y:0, w:700, h:400}) //open in new window
```

## openPage
Open URL(or execute HTML/JavaScript) in a new VisiOS window (or in a new actual window or a tab)
```js
// Open URL
VisiAPI('openPage', {url:'https://url_to_open'})

// Specify the size and starting coordinates
VisiAPI('openPage', {url:'https://url_to_open', w:700, h:500, x:100, y:10})

// HTML
VisiAPI('openPage', {html:'<h1>Hello!</h1><br><br>This is HTML!'})

// HTML + JS
VisiAPI('openPage', {html:'<h1>Hello!</h1><br><br>This is HTML!', script:'alert("Wow!")'})

// HTML for a new tab (*You cannot use JavaScript for this)
VisiAPI('openPage', {type:'newTab', html:'<h1>Hello!</h1><br><br>This is HTML!'})

// HTML for a new popup window (*You cannot use JavaScript for this)
VisiAPI('openPage', {type:'newWindow', html:'<h1>Hello!</h1><br><br>This is HTML!'})

// You can also specify x, y, w, h
VisiAPI('openPage', {type:'newWindow', html:'<h1>Hello!</h1><br><br>This is HTML!', x:0, y:0, w:700, h:400})
```

## closeWindow
Close the current app
```js
VisiAPI('closeWindow')
```

Close a selected window 
```js
async function test(){
	let windowId = await VisiAPI('openFile', {desktopId: 3, path: 'My Documents'})
	VisiAPI('closeWindow', { desktopId: 3, windowId: windowId })
}
test()
```
```js
async function test(){
	let windowId = await VisiAPI('openPage', {html: '<h1>Hello!</h1><br><br>This is HTML!'})
	VisiAPI('closeWindow', { windowId: windowId })
}
test()
```

---

<div id="user-content-toc">
	<ul align="center" style="list-style: none;">
		<summary>
			<h1>Storage APIs</h1>
		</summary>
	</ul>
</div>

## localStorage_set
If you pass a key name and value, this will add that key to the local storage, or update that key's value if it already exists.
If it's just temporary, consider to use memStorage_set instead since it's more faster and doesn't use up the browser storage.
You shouldn't rely on the local storage too much since the data will be lost when the user clear the browser cache.
To avoid that, use the appStorage_set instead.

```js
VisiAPI('localStorage_set', {n:'test_key', v:'Wow!!'})
```

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


## memStorage_set
If you pass a key name and value, this will add that key to the memory storage, or update that key's value if it already exists.
The memory storage is shared among all the VisiOS apps and is cleared when the user closes the tab.

```js
VisiAPI('memStorage_set', {n:'test_key', v:'Wow!!'})
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



## appStorage_set
If you pass a key name and value, this will add that key to the app storage, or update that key's value if it already exists.
If it's just temporary, consider to use memStorage_set instead since it's more faster and doesn't use up the VisiOS storage.

```js
VisiAPI('appStorage_set', {n:'test_key', v:'Wow!!'})
```

## appStorage_get
If you pass a key name, this will return the key's value from the app storage, or null if the key does not exist.

```js
async function test(){
	VisiAPI('appStorage_set', {n:'test_key', v:'Wow VisiOS!!'})
	let v = await VisiAPI('appStorage_get', {n:'test_key'})
	alert( v ) //wow!!
}
test()
```

