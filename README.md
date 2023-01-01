# Regular Expression Cheat Sheet - PCRE 

|Anchor|Description|Example|Valid match|Invalid|
:---|:---|:---|:---|---
^|start of string but in multiline mode it's the start of every line|^foam|foam|bath foam|
\A|start of string in any match mode (multiline mode m and singleline mode s) |\Afoam|foam|bath foam|
$|end of string but in multiline mode it's the end of every line|finish$|finish|finnish|
\Z|end of string, or char before last new line in any match mode|finish\Z|finish|finnish|
\z|end of string, in any match mode.|
\G|end of the previous match or the start of the string for the first match|\^(get\|set)\|\G\w+$|setValue|seValue
\b|[^A-Za-z0-9_] word boundary; position between a word character (\w), and a nonword character (\W)|\bis\b|This island is beautiful|This island isn't beautiful
\B|not-word-boundary.|\Bland|island|peninsula

|Assertion|Description|Example|Valid match|Invalid|
:---|:---|:---|:---|---
(?!...)|negative LOOKAHEAD|Suppose you want to match an y that is not followed by x . In other words you want to match an x only and only if there is not y after it. The regex for this will be /x(?!y)/ |xnot(y)| xy
(?=...)|positive LOOKAHEAD|Suppose you want to match an y followed by x . In other words you want to match an x only and only if there is  y after it. The regex for this will be /x(?=y)/ |xy| xnot(y)
(?<=...)|positive LOOKBEHIND|Suppose you want to match an x which immediately follows y. In other words you want to match an x only and only if there is  y before it. The regex for this will be/(?<=y)x/ | xy| not(x)y
(?<!...)|negative LOOKBEHIND |/(?<!x)y/ will match y in ay and by but it will not match xy. Or we can say it will not match y in xy, other wise it will match every y which doesn't have an x before it.| not(x)y | xy 

|Char class|Description|Example|Valid match|Invalid|
:---|:---|:---|:---|---
[ ]|class definition|[axf]|a, x, f|b
[ - ]|class definition range|[a-c]|a, b, c|d
[ \ ]|escape inside class|[a-f\.]|a, b, .| g
[^ ]|Not in class|[^abc]|d, e| a
[:class:]|POSIX class|[:alpha:]|string|0101
.|match any chars except new line|b.ttle|battle, bottle| bttle
\s|white space, [\n\r\f\t ]|good\smorning|good morning|good.morning
\S|no-white space, [^\n\r\f\t]|good\Smorning|good.morning|good morning
\d| digit|\d{2}|23|1a
\D| non-digit|\D{3}|foo, bar|fo1
\w| word, [a-z-A-Z0-9_]|\w{4}|v411|v4.1
\W|non word, [^a-z-A-Z0-9_]|.$%?|.$%?|.ab?

|Special character|Description
:---|:---
\\|general escape|
\n|new line|
\1|BackReference|
\r|carriage return|
\t|tab|
\v|vertical tab|
\f|form feed|
\a|alarm|
[\b]|backspace|
\e|escape|
\cchar|Ctrl + char(ie:\cc is Ctrl+c)
\ooo|three digit octal (ie: \123)
\xhh|one or two digit hexadecimal (ie: \x10)
\x{hex}|any hexadecimal code (ie: \x{1234})
\p{xx}|char with unicode property (ie: \p{Arabic}
\P{xx}|char without unicode property

|Sequence|Description|Example|Valid match|Invalid|
:---|:---|:---|:---|---
\||alternation|apple\|orange|apple, orange|melon
( )| subpattern |foot(er\|ball)|footer or football|footpath
(?P\<*name*>...)|subpattern, and capture submatch into *name*|`(?P<greeting>hello)`|hello|hallo
(?:...)|subpattern, but does not capture submatch|(?:hello)|hello|hallo
+| one or more quantifier|ye+ah|yeah, yeeeah|yah  
*| zero or more quantifier|ye*ah|yeeah, yeeeah, yah|yeh 
?| zero or one quantifier|yes?|yes, ye|yess  
??| zero or one, as few times as possible (lazy)|yea??h|yeah|yeaah|
+?| one or more  lazy |`/<.+?>/g`|`<P>foo</P>` matches only `<P>` and `</P>`|  
*?| zero or more, lazy|`/<.*?>/g`|`<html>`|
{n}|n times exactly|fo{2}|foo|fooo
{n,m}|from n to m times|go{2,3}d|good,goood|gooood
{n,}|at least n times|go{2,}|goo, gooo|go
(?(condition)...)|if-then pattern|`(<)?[p](?(1)>)`|`<p>`, p|<p
(?(condition)...\|...)|if-then-else pattern|`^(?(?=q)que|ans)`|question, answer|quote

|Pattern modifier|Description|
:---|:---
g| global match
i| case-insensitiv, match both uppercase and lowercase
m| multiple lines In multi-line mode, the ^ and $ anchors match the beginning and end of each line in the input string, rather than the beginning and end of the entire string. This can be useful when working with text that contains multiple lines, such as a block of code or a document.
s| single line (by default)
x| ingore whitespace allows comments
A| anchored, the pattern is forced to ^
D| dollar end only, a dollar metacharacter matches only at the end 
S| extra analysis performed, useful for non-anchored patterns
U| ungreedy, greedy patterns becomes lazy by default
X| additional functionality of PCRE (PCRE extra)
J| allow duplicate names for subpatterns
u| unicode, pattern and subject strings are treated as UTF-8 The \u flag in a regular expression is used to enable Unicode support in the pattern. When the \u flag is present, the regular expression engine will treat the pattern as a Unicode pattern and will attempt to match Unicode characters in the input string.

                                                               
                                                               
| Concept                 | Description                                                                                                                                                                                                                                                                                                                             |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| The U Flag              | In regular expressions, the `U` flag is used to enable Unicode-aware processing. When this flag is set, the regular expression will treat certain characters and character classes as Unicode characters, rather than as ASCII characters.                                                                                            |
| Unicode                  | Unicode is a character set that represents the majority of the world's written languages. It includes support for over 137,000 characters, including the ASCII character set, and is designed to be compatible with a wide range of devices and systems.                                                                                |
| Unicode Block            | A range of Unicode code points that represent a specific set of characters or symbols. There are many different Unicode blocks, each with its own range of code points and associated characters.                                                                                                                               |
| Unicode character properties | Metadata associated with Unicode characters that describe certain characteristics or features of the characters. These properties can be used to classify or identify characters in various ways, such as by their script, category, or general category. Examples include `Script`, `Category`, `General_Category`, `Uppercase`, and `Lowercase`. |
| Code Points              | A numerical value assigned to each Unicode character, which represents the character's position in the Unicode code space. Code points are typically represented in hexadecimal notation, and can range from `U+0000` to `U+10FFFF`.                                                                                                     |
| ASCII                    | ASCII (American Standard Code for Information Interchange) is a character set that represents 128 specific characters, including the numbers 0-9, the uppercase and lowercase letters of the alphabet, and various special characters such as punctuation marks and symbols.                                                                |
| UTF-8                    | UTF-8 (Unicode Transformation Format - 8-bit) is a character encoding system that represents the Unicode character set using 8-bit code units. It is designed to be backwards-compatible with ASCII, which means that ASCII characters are encoded using the same values as in ASCII, but UTF-8 also includes support for a much wider range of characters, including those from many different languages and scripts. |
                                                               

                                                               
