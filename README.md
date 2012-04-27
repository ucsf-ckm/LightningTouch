Lightning Touch
===============

Lightning Touch makes links responsive without the several hundred millisecond delay typical in a hendheld touchscreen browser.

To see it in action, check out the **Sites That Use Lightning Touch** section below.

## Quick Start

1. Put `LightningTouch.js` (or better yet, the minified version in the `demo` directory) in a sensible place on your web server. 
2. In the web page that you wish to make Lightning Touch-enabled, link to the Lightning Touch JS file. For example:

```
<script src="/js/LightningTouch-1.0.0.min.js"></script>
```

3. If your site has consistent header, footer, navigation, or other content that exists in its own block element, you can leave that stuff alone and it will appear on all the pages that result from Lightning Touch.
4. Take the main content of each of your pages and:
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

5. Indicate the id of your default/main content with a `data-default-target-id` attribute on the `body` element.

```
<body data-default-target-id="lightning-main">
```

That's it! You should have some really fast links on touch-enabled devices like iPhones, iPads, Android devices, and Blackberry devices that are not ancient.

## Sites That Use Lightning Touch

* [UCSF Mobile](http://m.ucsf.edu/)

## FAQ

### How do I implement a fallback for browser's that can't do Lightning Touch?

Browsers that do not work with Lightning Touch (e.g., Internet Explorer) will go to the URLs specified in the `href` attribute of the anchors as usual. This does mean you need to have your content available in two places. A template engine or other dynamic content generation mechanism can reduce or eliminate the need to repeat the content in two places.

### How do I track page loads via Lightning Touch using Google Analytics?

Add an event listener for `hashchange`:

```
window.addEventListener('hashchange', function() { _gaq.push(["_trackPageview", window.location.hash])}, false);
```

You can use `substr()` to strip off the hash mark and the prepended slash if you prefer. This is especially useful if your `id` attributes always correspond to your `href` values and you would like them to be treated as the same thing by Google Analytics.

```
window.addEventListener('hashchange', function() { _gaq.push(["_trackPageview", window.location.hash.substr(2)])}, false);
```

## Miscellania

Lightning Touch is made available via the New BSD License.

The copyright for Lightning Touch is owned by the Regents of the University of California. All rights reserved.

Lightning Touch was written by Rich Trott at the UCSF Library and Center for Knowledge Management.  You can find him on Twitter: `@trott`