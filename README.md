# BackShadow
full screen cover up for overlayed UI components with Meteor Blaze.

![Backshadow screenshot](https://raw.githubusercontent.com/Pushplaybang/backshadow/master/assets/screenshot.jpg)



## Install
Simply install the package via atmosphere

```sh
meteor add pushplaybang:backshadow
```



## Usage

```js
{{> backShadow id='navigation' }}
```

the `id` parameter is essential in order to provide a unique context for the backshadow instance. Once this is in your 

Once your tempalte is setup, you can open and close the backshadow with the following methods:

```js
BackShadow.open('navigation');
BackShadow.close('navigation');
```

Both of these methods accept a set of parameters parameter, the only essential one is the `id` which should match what you specified in the template.

### Arguments
The open and close methods accept the following parameters, the `id` is the only required argument:

```js
BackShadow.open(id, data, callback, callbackStack);
```

 - `id` (string) the id set on the backshadow template you want to interact with
 - `data` (object) an opbject to emit with the open event
 - `callback` (function) a function to call when opening the backshadow
 - `callbackstack` (function / array / object) a function or set of functions to be called when the backshadow element is closed

```js
BackShadow.close(id, data, callback);
```

 - `id` (string) the id set on the backshadow template you want to interact with
 - `data` (object) an opbject to emit with the close event
 - `callback` (function) a function to call when closing the backshadow

### Additional Methods
The open and close methods mentioned above emit open and close events, sometimes you'll need to open or close the backshadow without triggering an event.  For this, there are two additional methods `hide` and `show` which only accept an `id` parameter.


## Events
BackShadow also provides events via `BackShadow.events` object.  these can be accessed in the following way,  notice that the events are namespaced with the id you passed to your template.  This makes it easy to orchastrate other actions along with the opening or closing of BackShadow.

```
BackShadow.on('navigation/open', function() {}); // callback on open event
BackShadow.on('navigation/close', function() {}); // callback on close event
```

I went with events here as its lighter than following a reactive pattern, as its likely you'll be animating one or more elements along with the usage of BackShadow. #thatSingleThreadLife.

Note that Backshadow also uses an SVG as it has better legacy support for pointer events.

Also note that clicking on the backshadow will close it and fire a close event, this is useful in most situations, but a override is in the works.

## Body Class
When backshadow opens it adds a class to the body in the format `js-backshadow-visible-<id>` allowing you to style other elements in the dom, usually behind the shadow, while its active.

### Contributions and Suggestions Welcome!
Have something you think this needs or could use as an improvement, let me know.  add [an issue on github](https://github.com/Pushplaybang/backshadow/issues) or fork and create a pull request.


## Changelog
This includes notable changes to the package

0.0.3
 - changed the body class from `backshadow-visible` to `js-backshadow-visible`
 - updated documentation to include the `show` and `hide` methods
 - added documentation of function params.

____


### License [MIT](https://opensource.org/licenses/MIT)
Copyright (c) 2016 Paul van Zyl

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.  IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.