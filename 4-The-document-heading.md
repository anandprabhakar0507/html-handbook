# The document heading

The `head` tag contains special tags that define the document properties.

It's always written before the `body` tag, right after the opening `html` tag:

```html
<!DOCTYPE html>
<html>
	<head>
		...
	</head>
	...
</html>
```

We never use attributes on this tag. And we don't write content in it.

It's just a container for other tags.
Inside it we can have a wide variety of tags, depending on what you need to do:

- `title`
- `script`
- `noscript`
- `link`
- `style`
- `base`
- `meta`

### The `title` tag

The `title` tag determines the page title. The title is displayed in the browser, and it's especially important as it's one of the key factors for Search Engines Optimization.

### The `script` tag

This tag is used to add JavaScript into the page.

You can include it inline, using an opening tag, the JavaScript code and then the closing tag:

```html
<script>
..some JS
</script>
```

Or you can load an external JavaScript file by using the `src` attribute:

```html
<script src="file.js"></script>
```

> The `type` attribute by default is set to `text/javascript`, so it's completely optional.

There is something pretty important to know about this tag.

Sometimes this tag is used at the bottom of the page. Why? For performance reasons.

Loading scripts by default blocks the rendering of the page until the script is parsed and loaded.

Doing so, the script is loaded and executed after all the page is already parsed and loaded, giving a better experience to the user over keeping it in the `head` tag.

My opinion is that this is now bad practice. Let `script` live in the `head` tag.

In modern JavaScript we have an alternative, more performant than keeping the script at the bottom of the page - `defer` attribute:

```html
<script defer src="file.js"></script>
```

This is the scenario that triggers the faster path to a fast loaded page, and a fast loaded JavaScript.

> Note: the `async` attribute is similar, but in my opinion a worse option than `defer`. I describe why in details in the page  [https://flaviocopes.com/javascript-async-defer/](https://flaviocopes.com/javascript-async-defer/)

### The `noscript` tag

This tag is used to detect when scripts are disabled in the browser.

> Note: users can choose to disable JavaScript scripts in the browser settings. Or the browser might not support them by default.

It is used differently whether it's put in the document head, or in the document body.

We're talking about the document head now, so let's first introduce this usage.

In this case, the `noscript` tag can only contain other tags:

- `link` tags
- `style` tags
- `meta` tags

to alter the resources served by the page, or the `meta` information, if scripts are disabled.

In this example I set an element with the `no-script-alert` class to display if scripts are disabled, as it was `display: none` by default:

```html
<!DOCTYPE html>
<html>
	<head>
		...
		<noscript>
			<style>
				.no-script-alert {
					display: block;
				}
			</style>
		</noscript>

		...
	</head>
	...
</html>
```

> Let's solve the other case: if put in the body, it can contain content, like paragraphs and other tags, which are rendered in the UI.

### The `link` tag

The `link` tag is used to set relationships between a document and other resources.

It's mainly used to link an external CSS file to be loaded.

This element has no closing tag.

Usage:

```html
<!DOCTYPE html>
<html>
	<head>
		...
		<link href="file.css" rel="stylesheet">
		...
	</head>
	...
</html>
```

The `media` attribute allows to load different stylesheets depending on the device capabilities:

```html
<link href="file.css" media="screen" rel="stylesheet">
<link href="print.css" media="print" rel="stylesheet">
```

We can link to different resources than stylesheets.

For example we can associate an RSS feed using

```html
<link rel="alternate" type="application/rss+xml" href="/index.xml">
```

We can associate a favicon using:

```html
<link rel="apple-touch-icon" sizes="180x180" href="/assets/apple-touch-icon.png">

<link rel="icon" type="image/png" sizes="32x32" href="/assets/favicon-32x32.png">

<link rel="icon" type="image/png" sizes="16x16" href="/assets/favicon-16x16.png">
```

This tag _was_ also used for multi-page content, to indicate the previous and next page using `rel="prev"` and `rel="next"`. Mostly for Google. As of 2019, [Google announced it does not use this tag any more](https://twitter.com/googlewmc/status/1108726443251519489) because it can find the correct page structure without it.

### The `style` tag

This tag can be used to add styles into the document, rather than loading an external stylesheet.

Usage:

```html
<style>
.some-css {}
</style>
```


As with the `link` tag, you can use the `media` attribute to only use that CSS on the specified medium:

```html
<style media="print">
.some-css {}
</style>
```

You can also add this tag in the document body. Speaking of this, it's interesting the `scoped` attribute to only assign that CSS to the current document subtree. In other words, to avoid leaking the CSS outside of the parent element.

### The `base` tag

This tag is used to set a base URL for all relative URLs contained in the page.

```html
<!DOCTYPE html>
<html>
	<head>
		...
		<base href="https://flaviocopes.com/">
		...
	</head>
	...
</html>
```

### The `meta` tag

Meta tags perform a variety of tasks and they are very, very important.

Especially for SEO.

`meta` elements only have the starting tag.

The most basic one is the `description` meta tag:

```html
<meta name="description" content="A nice page">
```

This *might* be used by Google to generate the page description in its result pages, if it finds it better describes the page than the on-page content (don't ask me how).

The `charset` meta tag is used to set the page character encoding. `utf-8` in most cases:

```html
<meta charset="utf-8">
```

The `robots` meta tag instructs the Search Engine bots whether to index a page or not:

```html
<meta name="robots" content="noindex">
```

Or if they should follow links or not:

```html
<meta name="robots" content="nofollow">
```

> You can set nofollow on individual links, too. This is how you can set `nofollow` globally.

You can combine them:

```html
<meta name="robots" content="noindex, nofollow">
```

The default behavior is `index, follow`.

You can use other properties, including `nosnippet`, `noarchive`, `noimageindex` and more.

You can also just tell Google instead of targeting *all* search engines:

```html
<meta name="googlebot" content="noindex, nofollow">
```

and other search engines might have their own meta tag, too.

Speaking of which, we can tell Google to disable some features. This prevents the translate functionality in the search engine results:

```html
<meta name="google" content="notranslate">
```

The `viewport` meta tag is used to tell the browser to set the page width depending on the device width.

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

[See more on this tag](https://developer.mozilla.org/en-US/docs/Mozilla/Mobile/Viewport_meta_tag).

Another rather popular meta tag is the `http-equiv="refresh"` one. This line tells the browser to wait 3 seconds, then redirect to that other page:

```html
<meta http-equiv="refresh" content="3;url=http://flaviocopes.com/another-page">
```

Using 0 instead of 3 will redirect as soon as possible.

This is not a full reference, other less used meta tags exist.

After this document heading introduction, we can start diving into the document body.