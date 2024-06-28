
# Quantifiers
“quantifier” specifies how many times a certain character or group of characters should appear in the input string

| Quantifier | Description                               | Example                                                                                                                                                                                                                                                                                                         |
|------------|-------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| .          | Any single character except for a newline | .{2,} matches two or more of any character (except for newline characters), such as abcd, 123, @@, :D <br> a.b.{3}c: This pattern matches any string that has an 'a', followed by any character, followed by 'b', followed by three any characters, and then followed by 'c', such as a1b123c, axbxyzc, a€b世~@c |
| ?          | 0 or 1                                    | a.?z matches with az, abz, a1z, a$z                                                                                                                                                                                                                                                                                                                |
| +          | \>= 1                                     | a.+z matches with abz, abcdz, aaaaaaz                                                                                                                                                                                                                                                                                                               |
| *          | \>= 0                                     | a.*z matches with az, abz, abcdz, aaaaaaz                                                                                                                                                                                                                                                                                                           |
| {n}        | n                                         | a{3} matches with aaa                                                                                                                                                                                                                                                                                           |
| {n,}       | \>= n                                     | a{3,} matches strings with three or more consecutive ‘a’ characters. such as aaa, aaaa                                                                                                                                                                                                                          |
| {n, m}     | \>= n &&<= m                              | a{2,4} matches strings with 'a' repeated 2 to 4 times consecutively, such as aa, aaa, aaaa.                                                                                                                                                                                                                     |


## Greedy/lazy quantifiers

greedy ==>  + and * 

non-greedy ==> ?

Test String : some `<foo>` `<bar>` new `</bar>` `</foo>` thing:

<.*> will match `<foo>` `<bar>` new `</bar>` `</foo>`

<.*?> will match `<foo>`

## Escaping

\. matches a literal dot . , not matches with a, b

\? matches a literal question mark ?


# Flavours
    -    Regex flavors refer to the specific implementations or variations of regular expressions found in different programming languages or libraries. Each programming language or tool that supports regular expressions may have its own unique flavor, characterized by distinct features, syntax, and behavior

# Flags

| Flag                      | Description    |
|---------------------------|----------------|
| i (case-insensitive):     | the regex pattern becomes case-insensitive |
| g (global)                | The “g” flag allows the regex to find all matches within a given string, rather than stopping after the first match |
| m (multiline)             | Without the “m” flag, they match the start and end of the entire string. With the “m” flag, they match the start and end of each line within the string <br> The “m” flag changes the behavior of the ^ and $ anchors.|
| s (dotall or single line) | The “s” flag allows the dot . metacharacter to match any character, including newline characters. Without this flag, the dot matches any character except newlines. |


# Input boundary assertion (^ and $)

    -   ^ asserts that the current position is the start of input. $ asserts that the current position is the end of input
    -   If the m flag is not set, it is the start or end of the string. If the m flag is set, it is the start or end of a line.


# character set
    -   A character set, also called character class, is a group of characters enclosed in square brackets [ ]
    -   [0-9] matches any digit from 0 to 9
    -   [A-Za-z] matches any uppercase or lowercase letter
    -   [A-Za-z0-9] matches any alphanumeric character
    -   Inside the square brackets, you don’t need to escape metacharacters because they lose their special meaning
    -   The only symbol that has a meaning in the square brackets is a hyphen (-)
    -   However, the hyphen (-) is not treated as a metacharacter inside square brackets when it is placed in certain positions and contexts For example, [abcd-] and [-abcd] match the "b" in "brisket", the "c" in "chop", and the "-" (hyphen) in "non-profit".

# Negating a Character Set [^]
    -   [^characters_to_exclude]
    -   [^a-zA-Z] matches any character that is not an uppercase or lowercase letter.
    -   [^ \t\r\n] matches any character that is not a whitespace character (space, tab, carriage return, or newline).

# Shorthand Character Sets
    -   Shorthand character sets allow you to match common groups of characters without listing each individual character explicitly.
    -   \d matches any digit, equivalent to [0-9].
    -   \D matches any non-digit character, equivalent to [^0-9].
    -   \w matches any word character (alphanumeric character plus underscore), equivalent to [a-zA-Z0-9_].
    -   \W matches any non-word character, equivalent to [^a-zA-Z0-9_].
    -   \s matches any whitespace character (space, tab, newline, etc.).
    -   \S matches any non-whitespace character.

# Word boundary assertion
    -    A word boundary can occur in one of three positions:
         1. Before the first character in the string, if the first character is a word character.
         2. After the last character in the string, if the last character is a word character.
         3. Between two characters in the string, where one is a word character and the other is not a word character.
         Word characters are alpha-numeric; a minus sign is not.
    -   A word boundary assertion is used to specify a position in the text where a word begins or ends
    -   \b: Represents a word boundary that asserts the position where a word begins or ends.
    -   \B: Represents a non-word boundary, which asserts the position where a word does not begin or end.
    -   \bm matches the "m" in "moon".
    -   oon\b matches the "oon" in "moon", because "oon" is the end of the string, thus not followed by a word character.
    -   /ye\B/ matches "ye" in "possibly yesterday".

# Or condition using pipe character (|)
    -  | (pipe character) acts as a logical OR operator, allowing you to specify multiple alternative patterns that you want to match.
    -  ^(I|You)\s.*$ matches sentences that start with either “I” or “You”

# Capturing Groups
    -  Capturing groups allow you to treat a part of your regex pattern as a single unit
    -  Without using grouping: [a-z]\d[a-z]\d[a-z]\d
    -  Using grouping : ([a-z]\d){3}
    -  for dd-mm-yyyy, using (\d{1,2})-(\d{1,2})-(\d{4}) we can capture Date as Group 1, month as Group 2 and year as Group 3

# Backreferences

    -  Backreferences are a feature that allows you to reference and reuse the text captured by a capturing group within the same regex pattern
    -  you can reference a capturing group by using a backslash followed by the group number
    -  Group numbers are assigned based on the order of opening parentheses in the regex pattern, starting from 1
    -  (a|b|cd)\1 matches aa, bb or cdcd
    -  (\d)(.+)\1+\2? matches 1a1, 1a1a, 1a11, 1a11a1
    -  Duplicated words \b([A-Za-z]+) +\1\b

# Non-capturing groups
    -  It is also possible to make a group non-capturing
    -  (?:chars)
    -  for dd-mm-yyyy, using (?:\d{1,2}-){2}(\d{4}):\1 we capture only year, eg: 21-08-2020:2020

# Nested capturing groups

    - For nested capturing groups, the order of the groups is the same as the order of the left parentheses. 
    - For example, in this regex (\d{4})-((\d{3})-(\d{2})),
    - (\d{4}) is the first capturing group and is numbered 1.
    - ((\d{3})-(\d{2})) is the second capturing group and is numbered 2.
    - (\d{3}) is the first inner capturing group of the second group and is numbered 3.
    - (\d{2}) is the second inner capturing group of the second group and is numbered 4.

# Named capturing group
    - Named capturing groups allow you to assign names to your capturing groups, making it easier to reference
    - (?<name> ... )
    - using (?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})
    - (?<year>\d{4}) defines a named capturing group named "year" to capture a 4-digit year.
    - (?<month>\d{2}) defines a named capturing group named "month" to capture a 2-digit month.
    - (?<day>\d{2}) defines a named capturing group named "day" to capture a 2-digit day.

# Lookaround Assertions: Lookaheads and Lookbehinds
    - Lookaround assertions are non-capturing groups that return matches only if the target string is followed or preceded by a particular character.
    - positive lookahead, negative lookahead, positive lookbehind, and negative lookbehind assertions.
    

# Positive Lookahead (?=chars)
    - It asserts that a certain expression can be found at the right side of the current position
    - xyz(?=123) means match xyz only if it is followed by 123
    - What if we reverse x(?=y) to (?=y)x
        - The pattern (?=y) matches strings that are followed by ‘y’, but there is no string preceding it. Therefore, it will match an "empty string" before y
        - So, the pattern (?=y)y matches an empty string before ‘y’ and is immediately followed by the letter ‘y’. In simpler terms, it’s just the letter ‘y’.
        - Similarly, the pattern (?=y)x matches an empty string before ‘y’ and is immediately followed by the letter ‘x’, which is impossible
    - what if (?=.*y)x
        -   .*: Matches any sequence of characters (except for a new line).
        -   y: Matches the literal character 'y'.
        -   Together, .*y matches any string that has at least one character ‘y’.
        -   Therefore, (?=.*y) matches an empty string that ‘y’ comes after it.
        -   Finally, the pattern (?=.*y)x matches the single character 'x' in strings that ‘y’ comes after it such as in 'xy,' 'x123y,' and 'x1y2'.
    - In short, (?=.*y) is typically used to check if the string has at least one character ‘y
        -   (?=.*[a-z]).+ matches a string that has at least one lowercase character.
        -   (?=.*[A-Z]).+ matches a string that has at least one uppercase character.
        -   (?=.*\d).+ matches a string that has at least one digit.
        -   (?=.*[^A-Za-z0–9\s]).+ matches a string that has at least one special character except whitespace.
        -   password with a minimum of 8 characters, including at least one uppercase letter, one lowercase letter, one numeric digit, and one special character (excluding whitespace). ^(?=.*[A-Z])(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9\s]).{8,}$

# Negative Lookahead (?!chars)
    -   (?!chars)
    -   x(?!y) matches ‘x’ only if it is NOT followed by ‘y’.
    -   ^(?!http|https).+$ to match ftp://file.com

# Positive Lookbehind (?<=chars)
    -   (?<=chars)
    -   (?<=x)y indicates you want to match y only if there's x before it
    -   (?<=\$)\d+ to match $100

# Negative lookbehind (?<!chars)
    -   (?<!chars)
    -   the pattern (?<!x)y means do not match y if there's x before it. In this case vy would match, ny, would match, but never xy.
    -   ^.+(?<!js|css|html)$ to match file path that does not end with “js”, “css”, or “html”.



