# Markdown Syntax

## Headings

```markdown
# heading level 1
## heading level 2
### heading level 3
...
###### heading level 6
```

> # heading level 1
> ## heading level 2
> ### heading level 3
> ...
>
> ###### heading level 6

## Horizontal Rules

```markdown
up
---
down
```

> up
>
> ---
>
> down

## Paragraphs and Line Breaks

Paragraphs: use **blank line** to separate

Line break: `<br>`

```markdown
para1

para2,line1<br>
line2
```

> para1
>
> para2,line1<br>
> line2

## Style

```markdown
**bold**

*italic*

***bold and italic***
```

> **bold**
> 
> *italic*
> 
> ***bold and italic***

### Strikethrough [Extended Syntax]

```markdown
~~Strikethrough~~
```

> ~~Strikethrough~~

### Emoji [Extended Syntax]

```markdown
Gone camping! :tent: Be back soon. That is so funny! :joy:
```

> Gone camping! :tent: Be back soon. That is so funny! :joy:

## Blockquotes

```markdown
> blockquotes paragraph1
>
> blockquotes paragraph2
>
>> nested blockquotes
```

>  > blockquotes paragraph1
>  >
>  > blockquotes paragraph2
>  >
>  > > nested blockquotes

## Lists

```
1. order list
1. order list
2. order list

- unorder list
- unorder list
```

> 1. order list
> 1. order list
> 2. order list
>
> - unorder list
> - unorder list

### Task Lists [Extended Syntax]

```markdown
- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media
```

> - [x] Write the press release
> - [ ] Update the website
> - [ ] Contact the media

## Hyperlinks

### Links

```markdown
[Google.com](https://www.google.com/)

[Google.com](https://www.google.com/ "search engine")

[Google.com Reference-style Links][1]

[1]: https://www.google.com/ "search engine"

<https://www.google.com/>

<yuanpinzhou@gmail.com>
```

> [Google.com](https://www.google.com/)
> 
> [Google.com](https://www.google.com/ "search engine")
> 
> [Google.com Reference-style Links][1]
>
> [1]: https://www.google.com/ "search engine"
>
> <https://www.google.com/>
> <yuanpinzhou@gmail.com>

### Images

```
![](imgs/google-icon.png)

![Google.com](imgs/google-icon.png "Google it")

[![Google with link](imgs/google-icon.png "Google it")](https://www.google.com/)
```

>![](imgs/google-icon.png)
>
>![Google.com](imgs/google-icon.png "Google it")
>
>[![Google with link](imgs/google-icon.png "Google it")](https://www.google.com/)

### Heading IDs [Extended Syntax]

```markdown
### My Great Heading 1
### My Great Heading 2 {#custom-id}

This is [my great heading 1](#my-great-heading-1), another one is [here](#custom-id).
```

> ### My Great Heading 1
> ### My Great Heading 2 {#custom-id}
>
> This is [my great heading 1](#my-great-heading-1), another one is [here](#custom-id).

## Code

````markdown
`print('hello world')`
````

> `print('hello world')`

**Syntax Highlighting [Extended Syntax]**

````markdown
```python
print('hello world')
```
````

> ```python
> print('hello world')
> ```

## Tables [Extended Syntax]

```markdown
| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |

| Syntax      | Description | Test Text     |
| :---        |    :----:   |          ---: |
| Header      | Title       | Here's this   |
| Paragraph   | Text        | And more      |
```

> | Syntax    | Description |
> | --------- | ----------- |
> | Header    | Title       |
> | Paragraph | Text        |
>
> | Syntax    | Description |   Test Text |
> | :-------- | :---------: | ----------: |
> | Header    |    Title    | Here's this |
> | Paragraph |    Text     |    And more |

## Footnotes [Extended Syntax]

```markdown
Here's a simple footnote,[^1] and here's a longer one.[^bignote]

[^1]: This is the first footnote.

[^bignote]: Here's one with multiple paragraphs and code.

    Indent paragraphs to include them in the footnote.

    `{ my code }`

    Add as many paragraphs as you like.
```

> Here's a simple footnote,[^1] and here's a longer one.[^bignote]
>
> [^1]: This is the first footnote.
>
> [^bignote]: Here's one with multiple paragraphs and code.
>
>     Indent paragraphs to include them in the footnote.
>     
>     `{ my code }`
>     
>     Add as many paragraphs as you like.

## Definition Lists [Extended List]

```markdown
First Term
: This is the definition of the first term.

Second Term
: This is one definition of the second term.
: This is another definition of the second term.
```

> First Term
> : This is the definition of the first term.
>
> Second Term
> : This is one definition of the second term.
> : This is another definition of the second term.

## Useful inline HTML

### Comment

```markdown
<!-- This is an HTML comment in Markdown -->

<!--
Comment multiple lines,
like this.
-->
```

### Adjust Images

```markdown
![](imgs/google-icon.png "original image")

<img src="imgs/google-icon.png" title="zoom image" style="zoom:25%;" />

<img src="imgs/google-icon.png" title="resized image" width="200" height="50" />

<img src="imgs/google-icon.png" title="resized image" align="right">
```

>![](imgs/google-icon.png "original image")
>
><img src="imgs/google-icon.png" title="zoom image" style="zoom:25%;" />
>
><img src="imgs/google-icon.png" title="resized image" width="200" height="50" />
>
><img src="imgs/google-icon.png" title="resized image" align="right">

### Align Text Block

```markdown
<p align="center">
    This is a right aligned paragraph.
    Check it out.
</p>
```

> <p align="center">
>     This is a right aligned paragraph.
>     Check it out.
> </p>

