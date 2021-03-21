# Tutorial source
https://www.regular-expressions.info/tutorial.html
https://www.regular-expressions.info/quickstart.html

For testing expressions
https://regex101.com/

# Notes
### What is a regular expression
Basically, a regular expression is a pattern describing a certain amount of text.

	\b[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}\b

this pattern describes an email address. 

### Literal Characters
The most basic regular expression consists of a single literal character, such as ``a``

### Special Characters
2 characters with special meanings: the backslash `\`, the caret `^`, the dollar sign `$`, the period or dot ? , the vertical bar or pipe symbol `|`, the question mark `?`, the asterisk or star `*`, the plus sign `+`, the opening parenthesis `(`, the closing parenthesis `)`, the opening square bracket `[`, and the opening curly brace `{`, These special characters are often called “metacharacters”

If you want to use any of these characters as a literal in a regex, you need to escape them with a backslash

### Non-Printable Characters
You can use special character sequences to put non-printable characters in your regular expressio
Use `\t` to match a tab character (ASCII 0x09), `\r` for carriage return (0x0D) and `\n` for line feed (0x0A). More exotic non-printables are `\a` (bell, 0x07), `\e` (escape, 0x1B), `\f` (form feed, 0x0C) and `\v` (vertical tab, 0x0B). Remember that Windows text files use `\r\n` to terminate lines, while UNIX text files use `\n`.

### Character Classes or Character Sets
A “character class” matches only one out of several characters.
To match an a or an e, use `[ae]`. You could use this in gr`[ae]`y to match either gray or grey
gr`[ae]`y does not match graay, graey or any such thing. The order of the characters inside a character class does not matter.
Hyphen inside a character class to specify a range of characters. `[0-9]`
Typing a caret after the opening square bracket negates the character class. The result is that the character class matches any character that is not in the character class. `q[^x]` matches qu in question. 

### Shorthand Character Classes
`\d` matches a single character that is a digit, `\w` matches a “word character” (alphanumeric characters plus underscore), and `\s` matches a whitespace character (includes tabs and line breaks). 

### The Dot Matches (Almost) Any Character
The dot matches a single character, except line break characters.
`gr.y` matches `gray`, `grey`, `gr%y`, etc. Use the dot sparingly

### Anchors
Anchors do not match any characters. They match a position. `^` matches at the start of the string, and `$` matches at the end of the string
E.g. `^b` matches only the first b in bob.

### Alternation
Alternation is the regular expression equivalent of “or”. `cat|dog` matches cat in About cats and dogs. If the regex is applied again, it matches dog
 To create a regex that matches cat food or dog food, you need to group the alternatives: `(cat|dog) food`
 
 ### Repetition
 The question mark makes the preceding token in the regular expression optional. `colou?r` matches colour or color
 The asterisk or star tells the engine to attempt to match the preceding token zero or more times  `<[A-Za-z][A-Za-z0-9]*>` matches an HTML tag
 Use curly braces to specify a specific amount of repetition `\b[1-9][0-9]{2,4}\b` matches a number between 100 and 99999
 
 ### Greedy and Lazy Repetition
 The repetition operators or quantifiers are greedy. They expand the match as far as they can, and only give back if they must to satisfy the remainder of the regex. The regex `<.+>` matches `<EM>first</EM>` in `This is a <EM>first</EM> test`.
 
 ### Grouping and Capturing
 Place parentheses around multiple tokens to group them together. You can then apply a quantifier to the group. E.g. `Set(Value)?` matches Set or SetValue. How to access the group’s contents depends on the software or programming language you’re using. Group zero always contains the entire regex match.
 
 ### Backreferences
 Within the regular expression, you can use the backreference \1 to match the same text that was matched by the capturing group. `([abc])=\1` matches a=a, b=b, and c=c
 