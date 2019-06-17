# Lynda.com Course
- Thu Oct 20 2016 10:01
## Wildcharacter Metacharacter 
- Challenge: Something that matches:
silver sliver slider
- Code: `s...er`
- To test your code visual mode select code and press `//`
- **Note** double quotes do not need to be escapded with `/`

## Character Sets Metacharacter
- `[]` Indicates that we want to match only **ONE** of the characters inside
  of the brackets.
- The `-` is only a Metacharacter inside of `[]`. It is used to specify range
  of numbers or letters. You can specify more than one range at a time.
	- If you want to match it then you need to escape it inside of '[]'.
	- Example: `[0\-9]`. This would match, 0, -, and 9. Nothing else.
- `[a-z0-9]`. When specifying numbers it will only match**ONE** number. For
example: `[0-255]` will match: 0, 1, 2, and 5. **Thats it!**. It will not
match 48, 255. None of that.
- We want to match WINGS registers.
- Example: R8 r88 Rx55 L8 l88 L255 S8 s88 S255 F8 f88 F255
- Code: `[RrLlSs]([0-9]|[0-9][0-9]|[1-2][0-5][0-9])`
- Code: `[RrLlSs]([0-9]|[0-9][0-9]|[1-2][0-5][0-9])`
- Not sure how to do it yet. The above will only match 3 digit registers.
- There's also `^` carrot. Which when inside `[]` means negation. So **DO
  NOT** match chars specified.
- **Shorthand Character Sets**
	- Digit: **\d** matches a single digit 0–9. It may also match digits in other scripts, depending on the regex flavor.
	- Word Character: **\w** matches a single “word character” which includes letters, digits, underscores. It may also match other characters, depending on the regex flavor.
	- Whitespace Character: **\s** matches a single “whitespace character”. This includes spaces and line breaks, depending on the regex flavor.
	- Uppercase Letter: **\u** matches a single uppercase letter A–Z. It may also match uppercase letters in other scripts, depending on the regex flavor.
	- Lowercase Letter: **\l** matches a single lowercase letter a–z. It may also match lowercase letters in other scripts, depending on the regex flavor.
	- Hexadecimal Digit: **\h** matches a single hexadecimal digit (0–9, A–F, and a–f).
	- Horizontal Space Character: **\h** matches a single “horizontal whitespace character”, which includes the tab and any Unicode space separator.
	- Vertical Space Character: **\v** matches a single “vertical whitespace character”, which includes the line feed \n, carriage return \r, vertical tab \v, form feed \f, next line \u0085, line separator \u2028, and paragraph separator \u2029 characters. \v is traditionally used to match the vertical tab, which it still is in languages such as JavaScript, Python, and Ruby. But recent versions of Perl and PCRE treat \v as a shorthand that includes the vertical tab along with all other vertical whitespace.
	- Initial Character in XML Name: **\i** matches any character that can appear as the first character in an XML name.
	- Consecutive Character in XML Name: **\c** matches any character that can appear as the second or following character in an XML name.

