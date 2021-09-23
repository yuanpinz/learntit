# Markdown Syntax

## Basic Syntax

### Headings

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

### Horizontal Rules

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

### Paragraphs and Line Breaks

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

### Emphasis

```markdown
**bold**
*italic*
***bold and italic***
```

> **bold**
> *italic*
> ***bold and italic***

### Blockquotes

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

### Lists

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
> [Google.com](https://www.google.com/ "search engine")
> [Google.com Reference-style Links][1]
>
> [1]: https://www.google.com/ "search engine"
>
> <https://www.google.com/>
> <yuanpinzhou@gmail.com>

### Images

```
![Google.com](/imgs/google-icon.png)
![Google.com](/imgs/google-icon.png "Google it")
[![Google.com](/imgs/google-icon.png "Google it")](https://www.google.com/)
```

> ![Google.com](/imgs/google-icon.png)
> ![Google.com](/imgs/google-icon.png "Google it")
> [![Google.com](/imgs/google-icon.png "Google it")](https://www.google.com/)

## Extended Syntax

### Code

````markdown
`print('hello world')`

```python
print('hello world')
```
````

> `print('hello world')`
>
> ```python
> print('hello world')
> ```

### Tables

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

### Footnotes

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












































---

**Ref**[^1]

[^1]: [Markdown Guild](https://www.markdownguide.org/)

