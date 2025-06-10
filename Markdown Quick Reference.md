# Markdown Quick Reference

A quick guide to the most common Markdown syntax.

## Headings

To create a heading, add hash marks (`#`) in front of a word or phrase. The number of hash marks you use will determine the size of the heading.

```markdown
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6
```
*Best practice: Separate headings from other text with a blank line.*

---

## Text Formatting

| Style | Syntax | Example |
|---|---|---|
| Bold | `**Bold Text**` or `__Bold Text__` | **Bold Text** |
| Italic | `*Italic Text*` or `_Italic Text_` | *Italic Text* |
| Bold & Italic | `***Bold & Italic***` or `___Bold & Italic___`| ***Bold & Italic*** |
| Strikethrough | `~~Strikethrough~~` | ~~Strikethrough~~ |
| Highlight | `==Highlight==` | ==Highlight== |
| Subscript | `H~2~O` | H~2~O |
| Superscript | `X^2^` | X^2^ |

*Note: Highlight, subscript, and superscript are extended syntax and may not be supported by all Markdown applications.*

**Line Breaks:** To create a hard line break, end a line with two or more spaces, then press enter.

---

## Blockquotes & Horizontal Rules

**Blockquotes** are used to indicate quoted text. Use the `>` character before a line.

```markdown
> This is a blockquote.
>
> > This is a nested blockquote.
```

> This is a blockquote.
>
> > This is a nested blockquote.

**Horizontal Rules** create a thematic break. Use three or more asterisks, dashes, or underscores on a line by themselves.

```markdown
***
---
___
```

---

## Lists

### Unordered Lists

Use an asterisk (`*`), plus (`+`), or minus (`-`) for each list item.

```markdown
- First item
- Second item
- Third item
    - Indented item
    - Indented item
```
- First item
- Second item
- Third item
    - Indented item
    - Indented item

### Ordered Lists

Use numbers followed by a period. The actual numbers don't matter; Markdown will render them sequentially.

```markdown
1. First item
1. Second item
1. Third item
    1. Indented item
```
1. First item
2. Second item
3. Third item
    1. Indented item

### Task Lists

Task lists allow you to create a list of items with checkboxes. This is common in GitHub Flavored Markdown (GFM).

```markdown
- [x] Complete task
- [ ] Incomplete task
```
- [x] Complete task
- [ ] Incomplete task

---

## Links & Images

### Links

Create a link by wrapping the link text in brackets `[]` and the URL in parentheses `()`.

```markdown
[Markdown Guide](https://www.markdownguide.org)

A raw URL will often be auto-linked: https://www.markdownguide.org
```

[Markdown Guide](https://www.markdownguide.org)

**Internal Links (Anchors):** To link to a heading within the same document, use the auto-generated ID from that heading.

```markdown
[Go to the Tables section](#tables).
```
[Go to the Tables section](#tables).

### Images

Image syntax is similar to links but prefixed with an exclamation mark `!`.

```markdown
![A goat](https://upload.wikimedia.org/wikipedia/commons/b/b2/Hausziege_04.jpg "A goat looking at the camera")
```
![A goat](https://upload.wikimedia.org/wikipedia/commons/b/b2/Hausziege_04.jpg "A goat looking at the camera")

To make an image a link, wrap the image syntax in link syntax.
```markdown
[![A goat](https://upload.wikimedia.org/wikipedia/commons/b/b2/Hausziege_04.jpg)](https://en.wikipedia.org/wiki/Goat)
```

---

## Code

### Inline Code
Wrap code with backticks `` ` `` to display it inline.

```markdown
Use the `print()` function to display output.
```
Use the `print()` function to display output.

### Fenced Code Blocks
Use triple backticks ` ``` ` or triple tildes `~~~` to create a code block. You can specify the language for syntax highlighting.

````markdown
```python
def hello_world():
  print("Hello, world!")
```
````
```python
def hello_world():
  print("Hello, world!")
```

---

## Tables

Create tables with pipes `|` and hyphens `-`. Use colons `:` on the header separator line to define column alignment.

```markdown
| Left Align  | Center Align | Right Align |
|:------------|:------------:|------------:|
| Cell 1      | Cell 2       | Cell 3      |
| Cell 4      | Cell 5       | Cell 6      |
```

| Left Align  | Center Align | Right Align |
|:------------|:------------:|------------:|
| Cell 1      | Cell 2       | Cell 3      |
| Cell 4      | Cell 5       | Cell 6      |

---

## Miscellaneous

### Escaping Characters
To display a literal character that has special meaning in Markdown, use a backslash `\` before it.

```markdown
\*Without the backslash, this would be a bullet point.\*
```
\*Without the backslash, this would be a bullet point.\*

### Footnotes
Add a footnote to your text.[^1] The definition can appear anywhere in the document.[^2]

[^1]: This is the first footnote.
[^2]: This is the second footnote.

```markdown
A sentence with a footnote.[^1]
[^1]: This is the footnote's content.
```

### Emoji
Some Markdown processors support emoji shortcodes.

```markdown
That's hilarious! :joy:
```
That's hilarious! :joy: