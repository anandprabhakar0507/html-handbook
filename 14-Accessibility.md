# Accessibility

It's important we design our HTML with accessibility in mind.

Having accessible HTML means that people with disabilities can use the Web. Totally blind users, or users visually impaired. People that have hearing loss issues. There are a lot of different disabilities.

Unfortunately this topic does not take the importance it needs, and it doesn't seem as cool as others.

What if a person can't *see* your page, but still wants to consume its content? First, how do they do that? They can't use the mouse, they use something called a **screen reader**. You don't have to imagine that. You can try one now: Google provides the free [ChromeVox Chrome Extension](https://chrome.google.com/webstore/detail/chromevox/kgejglhpjiefppelpmljglcjbhoiplfn/). Accessibility must also take care of allowing tools to easily select elements or navigate through the pages.

Web pages and Web apps are not always built with accessibility as one of their first goals, and maybe version 1 is released not accessible but it's possible to make a web page accessible after the fact. Sooner is better, but it's never too late.

It's important and in my country, websites built by the government or other public organizations must be accessible.

What does this mean to make an HTML accessible? Let me illustrate the main things you need to think about.

> Note: there are several other things to take care about, which might go in the CSS topic, like colors, contrast and fonts. Or [how to make SVG images accessible](https://css-tricks.com/accessible-svgs/). I don't talk about them here.

## Use semantic HTML

Semantic HTML is very important and it's one of the main things you need to take care of. Let me illustrate a few common scenarios.

It's important to use the correct structure for heading tags. The most important is `h1`, and you use higher numbers for less important ones, but all the same-level headings should have the same meaning (think about it like a tree structure)

```js
h1
	h2
		h3
	h2
	h2
		h3
			h4
```

Use `strong` and `em` instead of `b` and `i`. Visually they look the same, but the first 2 have more meaning associated with them. `b` and `i` are more visual elements.

Lists are important. A screen reader can detect a list and provide an overview, then let the user choose to get into the list or not.

A table should have a `caption` tag that describes its content:

```html
<table>
  <caption>Dogs age</caption>
  <tr>
    <th>Dog</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Roger</td>
    <td>7</td>
  </tr>
</table>
```

## Use `alt` attributes for images

All images must have an `alt` tag describing the image content. It's not just a good practice, it's required by the HTML standard and your HTML without it is not validated.

```html
<img src="dog.png" alt="picture of my dog" />
```

It's also good for search engines, if that's an incentive for you to add it.

## Use the `role` attribute

The `role` attribute lets you assign specific roles to the various elements in your page.

You can assign lots of different roles: complementary, list, listitem, main, navigation, region, tab, alert, application, article, banner, button, cell, checkbox, contentinfo, dialog, document, feed, figure, form, grid, gridcell, heading, img, listbox, row, rowgroup, search, switch, table, tabpanel, textbox, timer.

It's a lot and for the full reference of each of them I give you [this MDN link](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles). But you don't need to assign a role to every element in the page. Screen readers can infer from the HTML tag in most cases.  For example you don't need to add a role tag to semantic tags like `nav`, `button`, `form`.

Let's take the `nav` tag example. You can use it to define the page navigation like this:

```html
<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/blog">Blog</a></li>
  </ul>
</nav>
```

If you were *forced* to use a `div` tag instead of `nav`, you'd use the `navigation` role:

```html
<div role="navigation">
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/blog">Blog</a></li>
  </ul>
</div>
```

So here you got a practical example: `role` is used to assign a meaningful value when the tag does not convey the meaning already.

## Use the `tabindex` attribute

The `tabindex` attribute allows you to change the order of how pressing the Tab key selects "selectable" elements. By defaults only links and form elements are "selectable" by navigation using the Tab key (and you don't need to set `tabindex` on them).

Adding `tabindex="0"` makes an element selectable:

```html
<div tabindex="0">
...
</div>
```

Using `tabindex="-1"` instead removes an element from this tab-based navigation, and it can be pretty useful.

## Use the `aria` attributes

ARIA is an acronym that means Accessible Rich Internet Applications and defines semantics that can be applied to elements.

### `aria-label`

This attribute is used to add a string to describe an element.

Example:

```html
<p aria-label="The description of the product">...</p>
```

I use this attribute on my blog sidebar, where I have an input box for search without an explicit label, as it has a placeholder attribute.

### `aria-labelledby`

This attribute sets a correlation between the current element and the one that labels it.

If you know how an `input` element can be associated to a `label` element, that's similar.

We pass the item id that describes the current element.

Example:

```html
<h3 id="description">The description of the product</h3>

<p aria-labelledby="description">
...
</p>
```

### `aria-describedby`

This attribute lets us associate an element with another element that serves as description.

Example:

```html
<button aria-describedby="payNowDescription" >Pay now</button>

<div id="payNowDescription">Clicking the button will send you to our Stripe form!</div>
```

### Use aria-hidden to hide content

I like a minimalistic design in my sites. My blog for example is mostly just content, with some links in the sidebar. But some things in the sidebar are just visual elements that don't add up to the experience of a person that can't see the page. Like my logo picture, or the dark/bright theme selector.

Adding the `aria-hidden="true"` attribute will tell screen readers to ignore that element.

## Where to know more

This is just an introduction to the topic. To know more, I recommend those resources:

- [https://www.w3.org/TR/WCAG20/](https://www.w3.org/TR/WCAG20/)
- [https://webaim.org](https://webaim.org/)
- [https://developers.google.com/web/fundamentals/accessibility/](https://developers.google.com/web/fundamentals/accessibility/)
