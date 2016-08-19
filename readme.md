# routeJS

This plugin handles routes for both hash and push state.

### How to add routes

To add route you simply call the add function, providing it with the actual route string, an optional id, and the callback. 

$.router.add(*route*, *[id]*, *callback*);
	
Example:

	// Adds a route for /items/:item and calls the callback when matched
	$.router.add('/items/:item', function(data) {
		console.log(data.item);
	});

or

	// Adds a route for /items/:item and calls the callback when matched, but also has
	// a reference to the routes id in $.router.currentId
	$.router.add('/items/:item', 'foo', function(data) {
		console.log(data.item);
	});

### How to change urls and trigger routes
You can also change the current url to a route, and thereby triggering the route by calling *go*.

$.router.go(url, title);

Example:
	
	// This will change the url to http://www.foo.com/items/mycoolitem and set the title to
	// "My cool item" without reloading the page. If using hashes instead, it will use the url
	// http://www.foo.com/#!items/mycoolitem.
	// If a route has been set that matches it, it will be triggered.
	$.router.go('/items/mycoolitem', 'My cool item');
	
### Reseting all routes

If you need to remove all routes (which is good when testing) you just call:

`$.router.reset();`

### Dealing with 404's

If a url is entered which doesn't fire a route callback (a.k.a. 404 Not Found) you can add your error callback to take that case and make it beautiful.

```js
$.router.addErrorHandler(function (url) {
	// url is the URL which the router couldn't find a callback for
	console.log(url);
});
```