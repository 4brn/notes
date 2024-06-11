> NEVER INCLUDE HTML IN MARKDOWN! (except maybe comment)

<!-- headings -->

# This is h1

## This is h2

### This is h3

#### This is h4 (don't use)

##### This is h5 (don't use)

###### This is h6 (don't use)

<!-- paragraphs -->

This is the first paragraph.

This is the second paragraph.
Still the same paragraph!

There's a\
line break "`\`" above me!

or

Two blank spaces at the end of the line count as a line break.  

<!-- unordered lists -->

- Item
- Item
- Item

> Use either `-`, `*` or `+`

<!-- ordered lists -->

1. Item
1. Item
1. Item

> Counts from 1 and upwards

or

5. Item
6. Item
7. Item

> Counts from 5 and upwards

> Ordered list starts with number, followed by either `.` or `)` (Don't mix them up).\
> Use `\` to escape lists

<!-- sublists -->

1. Item one
1. Item two
    1. Sub-item (4 spaces indentation)
    2. Sub-item (4 spaces indentation)
    3. Sub-item (4 spaces indentation)
        - Sub-Sub-item (4 spaces indentation)
        - Sub-Sub-item (4 spaces indentation)

        This is a paragraph (formatting breaks)
1. Item four

<!-- checkboxes -->

- [x] Milk
- [ ] Alcohol
- [x] Fruits
- [ ] Meat

<!-- verbatim blocks -->

```<language>
Use 3 backits (```)
```

or

~~~markdown
# Use 3 tildes (~~~)
# To nest code blocks

```bash
echo "Hello"
```
~~~

or

    Indent 4 spaces.
    Don't use this.

<!-- quotations -->

> I use arch btw.

Every line of the quote must start with an `>`

Quotation itself is a whole anoter markdown document

> - Item
>   - Sub-item

Can have indented quotes:

> Quote ...
>
> > Quote inside of quote

<!-- seperator -->

---

> (Don't get crazy with all the different options.)
***
- - -
****************

<!-- tables -->

- :-- left justification
- --: right justification
- :-: central justification

| Col1         | Col2     | Col3          |
| :----------- | :------: | ------------: |
| Left-aligned | Centered | Right-aligned |
| blah         | blah     | blah          |

Col 1 | Col2 | Col3
:-- | :-: | --:
Ugh this is so ugly | make it | stop

<!-- inline formatting -->

*Italic*
*Italic*

**Bold**
**Bold**

***Bold & Italic***
***Bold & Italic***
***Bold & Italic***

> Use either `*` or `_`.\
> Don't mix them.

<!-- strikethrough -->

~~This text is rendered with strikethrough.~~

<!-- links -->

1. <https://skilstak.io>

> explicit links > hyperlinks

2. [text](http://link.com/)

> Don't put space between any of the brackets

3. [text](http://link.com/ "hover/alt text")
4. [music](/music/). (Relative URL)

5. This [website] is the bomb. [This][website] one also. This [website][] too.

[website]: http://link.org/ "hover/alt text"
> The content of this definition is used above.

> Tip: put the reference links after the the paragraph and not at the bottom of the file.

<!-- image -->

![alt](./assets/cat.png)

![alt](http://link.com/dog.png)

![alt][image]

Text, text, more text...

[image]: dog.jpg "optional title"
