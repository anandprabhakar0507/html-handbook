# The document body

After the closing head tag, we can only have one thing in an HTML document: the `body` element.

```html
<!DOCTYPE html>
<html>
	<head>
		...
	</head>
	<body>
		...
	</body>
</html>
```

Just like the `head` and `html` tags, we can only have one `body` tag in one page.

Inside the `body` tag we have all the tags that define the content of the page.

Technically, the start and ending tags are optional. But I consider it a good practice to add them. Just for clarity.

In the next chapters we'll define the variety of tags you can use inside the page body.

But before, we must introduce a difference between block elements and inline elements.

## Block elements vs inline elements

Visual elements, the ones defined in the page body, can be generally classified in 2 categories:

- block elements (`p`, `div`, heading elements, lists and list items, ...)
- inline elements (`a`, `span`, `img`, ...)

What is the difference?

Block elements, when positioned in the page, do not allow other elements next to them. To the left, or to the right.

Inline elements instead can sit next to other inline elements.

The difference also lies in the visual properties we can edit using CSS. We can alter the width/height, margin, padding and border of block elements. We can't do that for inline elements.

> Note that using CSS we can change the default for each element, setting a `p` tag to be inline, for example, or a `span` to be a block element.

Another difference is that inline elements can be contained in block elements. The reverse is not true.

Some block elements can contain other block elements, but it depends. The `p` tag for example does not allow such option.
