# headers
h1 header
=========
h2 header
---------

# blockquotes
> first level and paragraph
>> second level and first paragraph
>
> first level and second paragraph

# lists
## unordered - use *, +, or -
        * Red
        * Green
        * Blue

## ordered
        1. First
        2. Second
        3. Third

# code - use 4 spaces/1 tab
regular text
        code code code
or:
Use the `printf()` function

# hr's - three or more of the following
***
`---`
`___`

# links
This is [an example](http://example.com "Title") inline link.

# emphasis
*em* _em_

**strong** __strong__

# Tables
- Use vim-table-mode
- Example:
| Option Name        | Variable Type | Default             | Example                   |
|--------------------|---------------|---------------------|---------------------------|
| Installed          | Integer       | 0                   | Installed = 1             |
| PowerLineFrequency | Float         | 60.0                | PowerLineFrequency = 60.0 |
| Options            | String        | ""                  | Options = "Simulate=1"    |
| Model              | String        | ""                  | Model = "PXI NI-4071"     |
| NiDmmSoftPanel     | String        | See Example Section | See example Section       |

# Pandoc
- [Tips and Tricks](https://github.com/jgm/pandoc/wiki/Pandoc-Tricks)
- Installation `choco install pandoc` || `install pandoc`
- Excellent template for markdown [here](https://github.com/Wandmalfarbe/pandoc-latex-template)
- Convert markdown files to other formats
- Doesnt play well with tables though
- `pandoc test1.md -s -o test1.docx`
- `pandoc test1.md -s -o test1.pdf`
- Extention: `pipe_tables`
- Or you could just Print from google chrome to pdf

# To see markdown files
- Install Markdwon Reader Chrome extention
- AND 
After install, enable "Allow access to file URLs" in Extensions (menu > More tools > Extensions or enter URL chrome://extensions/ instead).

# Latex Install
- `choco install miktex` || `install texlive-most`

# Picture
![picture name](picture path.jpg)
![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")
