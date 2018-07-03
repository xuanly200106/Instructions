# Markdown Consultation

* * *

## Relationships with HTML
- For any markup that is not covered by Markdown's syntax, use HTML.
- Block-level HTML elements: Markdown formatting syntax is not processed within the tags
    + for example, `<div>`, `<table>`, `<pre>`, `<p>`
    + Seperate from surrounding content by blank lines
    + Start and end tags are not indented with tabs or spaces
- Span-level HTML tags can be used anywhere
    +  for example,  `<span>`, `<cite>`, or `<del>`
- No worry about Special character in HTML:  `<`, `&`
    + `<` : in HTML start tags, should be written as `'&lt;'`
    + `&` : in HTML denote entities, should be written as `'&amp;'`
    + Markdown will automatically recognize and translate these special characters
    + Inside span and block, always translate automatically

* * *  

## Block Element
### Paragraphs and line breaks  
- Paragraph definition: text separated by one or more blank lines(normal ones should not be indented with spaces or tabs).
- "hard-wrapped"(means line break in Markdown do not corresponds to the line break in output file), and use line ended with two or more spaces to insert `<br />`

### Headers
- Supports two styles
    +  Setext-style: (any number works, below header)
        *  `=======`below header means first-level
        *  `--------` below headers means second level
    +  Atx-style:
        *   use 1-6 hash(`#`) at start of the headers
        *   number of hash means the level of header
        *   can add random number of hash after header to close it(just for better appearance)

### Block Quotes
- Using `>` at the start of quoting
- `>` can be put before each line, or just before the hard-wrapped paragraph
- `>` can be nested, can have several quote structures using multiple `>`
- can contain other elements, including headers, lists, code blocks

### Lists
- Unordered form: using `+` `*` `-` to notes the lists
- Ordered form: using numbers followed by periods `1. `
    + the denoting number has no effect on the final output files
    + so can use random numbers to order the line
- Markers can be indented by up to three spaces
- List Markers must be followed by one or more spaces or tabs
- Blank line means `<p>` tags in HTML (have a line vertical space output before and between each lists)
- Subsequent paragraph in a list must be indented by either 4 spaces or one tab
- The blockquote sign `>` also need to be indented
- CodeBlock need to be indented twice(4+4)
- To avoid trigger ordered list, can use form `1\.`

### Code Blocks
- indent each line with 4 spaces or 1 tab
- In HTML, it corresponds to `<pre><code> Contents </code></pre>`
- Within code blocks, `&` and `<>` are automatically converted

### Horizontal Rules
- Produce horizontal rule tag(`<hr />`) by three or more hyphens,asterisks, or underscores
- `* * *` `- - -` `___`
- can place spaces between the hyphens or asterisks

* * * * * * * * 
## Span Elements

### Links
- Sopports two styles of links, text is delimited by square brackets `[]`
    + inline style:
        * Text which link corresponds to is delimited by `[]` 
        * Regular parentheses `()` immediated after square brackets
        * Inside `()`, is URL along with *optional* title surrounded in quotes
        * `[an example](https://URL/ "Title")`
        * when refer to a local source, can use relative paths for URL `(/about/ "Title")`
    + reference style:
        * use a second set of square brackets, inside is the label
        * there an be an optional space between two brackets
        * `[an example] [id]`
        * anywhere in the doc, can define the id URL
            - `[id]:` followed by one or more spaces
            - Title can be delimited by double or single quotes `"` `'` or parentheses `()`
            - URL can be optionally surrounded by angle brackets `<>`
        * `[id]: URL "Optional Title"`
        * id is not case sensitive, can contain everything
        * `[example][]` is an *implicit link name*, use the text itself as an id
        * The id definition can be put anywhere, normally immediately after the paragraph

### Emphasis
- using asterisks `*` and underscore `_`
- wrapped with one: `<em>` tag, Itatic
- wrapped with two: `<strong>` tag, Bold
- if surround `*` or `_` with spaces, then it is treated literally
- To avoid accidentally use emphasis, use `\*` and `\_` instead.

### Code
- using backtick quote ``
- to include a backtick quote inside the code, can use multiple backticks as delimiters ``` ``There is a literal backtick (`) here`` ```
- one space after opening and one before closing is allowed
- within code, ampersands and angle brackets are transfered automatically


### Images
- Inline form:
    + `![text](/path/to/img.jpg)`
    + `![Alt text](/path/to/img.jpg "Optional title")`
- Reference form:
    + `![Alt text][id]`
    + `[id]: url/to/image  "Optional title attribute"`
- Just add an exclamation `!` before the normal links

## Miscellaneous(other aspects)
### Automatic links
- surround the URL with angle brackets `<>`

### Blackslash escapes
- using backslash `\` to generate literal characters
- can work for following characters:  
        `\`   backslash  
        `` ` ``   backtick  
        `*`   asterisk  
        `_`   underscore  
        `{}`  curly braces  
        `[]`  square brackets  
        `()`  parentheses  
        `#`   hash mark  
        `+`   plus sign  
        `-`   minus sign (hyphen)  
        `.`   dot  
        `!`   exclamation mark  

## Extended Application
### Github Flavored Markdown
- [Document](https://help.github.com/articles/basic-writing-and-formatting-syntax/ "Github Markdown File")
    + Strikethrough : `~~TEXT~~`
    + Table  
    ```
    | First Header  | Second Header |  
    | ------------- | ------------- |  
    | Content Cell  | Content Cell  |  
    | Content Cell  | Content Cell  |  
    ```
    + Code highlight
    If you denote coding language inside the code, then you will have highlight automatically
    ````
    ```Python
    Code
    ```
    ````

### Way to see realtime refreshing preview
- adding  `<meta http-equiv="refresh" content="0.5">` at the end of the md files
- `ctrl+shift+P` and use autosave only in current files
- `ctrl+B` and you can see files refreshing automatically

