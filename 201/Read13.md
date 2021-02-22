# Local storage
Local storage is one advantage that the native client applications have over web applications, web applications use cookies for storing information, while cookies are included with every HTTP request, that will cause the web application to slow down and it will send data unencrypted over internet and they are limited to only 4 KB of data.
### HTML5 storage
It’s a way for web pages to store named key/value pairs locally, within the client web browser, the data will stay even when the user exits the website, but this data will never be transmitted to the remote web server.
Most browsers supports HTML5 storage, but there are some that don’t so we can check support by using :
If( Modernizr.localstorage ) {
} else {
}.
The HTML5 storage is based on name key/value pairs, data is stored on a named key, and will be retrieved by the same key.
The key is a string and the data can be any type supported by JS such as 
* Booleans.
* Integers.
* Strings.
* Floats.
If data is stored in a type other than string we need to use functions such as parseInt() or parseFloat() to retrieve data into the expected JS datatype.
There are also methods for removing the value for a given named key, and clearing the entire storage area (that is, deleting all the keys and values at once), so we use removeItem().
And there is a property to get the total number of values in storage area by using key(index).
If you want to keep track programmatically of when the storage area changes, you can trap the storage event. The storage event is fired on the window object whenever setItem(), removeItem(), or clear() is called and actually changes something. For example, if you set an item to its existing value or call clear() when there are no named keys, the storage event will not fire, because nothing actually changed in the storage area.
In HTML5 the storage space each origin gets by default is *5MB*, and if the storage exceeds that limit an exception called **“ QOUTA_EXCEEDED_ER “** will appear.
Storage in action
As an example when we use HTML5 in games, the progress will be stored even if the user exits the game without finishing it as they didn’t leave it.
