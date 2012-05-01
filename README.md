Lightning Touch
===============

Lightning Touch makes links responsive without the several hundred millisecond delay typical in a hendheld touchscreen browser.

To see it in action, check out the **Sites That Use Lightning Touch** section below.

## Using Lightning Touch

* Put `LightningTouch.js` (or better yet, the minified version in the `demo` directory) in a sensible place on your web server. 
* In the web page that you wish to make Lightning Touch-enabled, link to the Lightning Touch JS file. For example:

```
<script src="/js/LightningTouch-1.0.0.min.js"></script>
```

* If your site has consistent header, footer, navigation, or other content that exists in its own block element, you can leave that stuff alone and it will appear on all the pages that result from Lightning Touch.
* Take the main content of each of your pages and:
   * Wrap it in a block element (e.g., `<div>`). Assign a value to the `id` attribute. Use inline style or a stylesheet to set `display:none`. (Shameful admission: I've only tested this extensively with inline styles. For stylesheets, my testing has been minimal. If you use it with stylesheets, let me know the results!)
   * Take each anchor (`<a>`) element that you wish to Lightning Touch-enable and add a `data-target-id` indicating the `id` of the block element that anchor should link to. (Don't worry; `data-target-id` is a totally valid attribute in HTML5.)

```
<div id="lightning-main" style="display:none">
  <h1>Lightning Touch</h1>
  <h2>Awesomeness!</h2>
  <a href="awesome.html" data-target-id="awesome">Tap for Lightning Touch!</a>
</div>

<div id="awesome" style="display:none">
  <h1>Whoa!</h1>
  <h2>That was awesome!</h2>
  <a href="main.html" data-target-id="lightning-main">Go back to main page!</a>
</div>
```

* Indicate the id of your default/main content with a `data-default-target-id` attribute on the `body` element.

```
<body data-default-target-id="lightning-main">
```

That's it! You should have some really fast links on touch-enabled devices like iPhones, iPads, Android devices, and Blackberry devices that are not ancient.

## Sites That Use Lightning Touch

* [UCSF Mobile](http://m.ucsf.edu/)

## Additional Usage Notes

### Fallback

Browsers that do not work with Lightning Touch (e.g., Internet Explorer) will go to the URL specified in the `href` attribute of the anchor as usual. This does mean you need to have your content available in two places. A template engine or other dynamic content generation mechanism can reduce or eliminate the need to repeat the content in two places.

### Reducing Payload

Every visitor will load all the Lightning Touch-enabled content on every visit. Consider using [HTML5 offline appcaching](http://www.html5rocks.com/en/tutorials/appcache/beginner/) to mitigate the network payload.

### Google Analytics

To track Google Analytics Lightning Touch "page" loads, add an event listener for `hashchange`:

```
window.addEventListener('hashchange', function() { _gaq.push(["_trackPageview", window.location.hash])}, false);
```

You can use `substr()` to strip off the hash mark and the prepended slash if you prefer. This is especially useful if your `id` attributes always correspond to your `href` values and you would like them to be treated as the same thing by Google Analytics.

```
window.addEventListener('hashchange', function() { _gaq.push(["_trackPageview", window.location.hash.substr(2)])}, false);
```

## License

Copyright (c) 2012, Regents of the University of California
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
* Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
* Neither the name of the University of California nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY
DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

## Notes

Lightning Touch was written by Rich Trott at the [UCSF Library and Center for Knowledge Management](http://library.ucsf.edu).  You can find him on Twitter: [@trott](http://twitter.com/trott)

Lightning Touch started with a portion of [fastButtons](http://code.google.com/mobile/articles/fast_buttons.html) created and shared by Google and used according to terms described in the Creative Commons 3.0 Attribution License.