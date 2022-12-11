# Ready for Regex!!

So, you wanna learn about regex. What even is that? How do you use it? Is it a videogame item? All valid questions; and questions I had when I first heard about this. ESPECIALLY the videogame item part. Sounds like a cool weapon, honestly.

 This is where I've done research into the topic myself so I can return to you what I've gathered. I hope this is helpful to you  as it was for me. Down below are the different parts that make up a regex. Let's get started!

## Summary

Regex is short for 'regular expression', which is a string of characters used to search certain patterns. Very similiar to using the 'Find' tool on a website, except this can also validate things like passwords and email addresses. Super helpful for data. Here's an example:

/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

I know it looks like my cat jumped on my keyboard; but this is an example of a regular expression being used to validate an email. We'll break this down later. But the 'character soup' look will be a consistent thing.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

### Anchors

There are two anchors used in regular expressions ^ and $. Anchors are characters that specify to look for the string that comes after (^) or before ($) the anchor. 
So, if your search was '^but', then just 'but' and 'but wait!' would come up; but not a capital 'But', because no one starts a sentence with 'but'. The main reason is because regex is case-sensitive.

/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

So in this expression, the two aanchors are at the beginning and end of the sequence. Meaning It's specifically looking for everything in between. Super helpful, I know.

### Quantifiers

These set the limit of the string, or section of it, that our regex will match. You know how when you make a new account and it says it must be '6' characters long? This a quantifer at work. 

    * — Matches the pattern zero or more times

    + — Matches the pattern one or more times

    ? — Matches the pattern zero or one time

    {} — Curly brackets can provide three different ways to set limits for a match:

    { n } — Matches the pattern exactly n number of times

    { n, } — Matches the pattern at least n number of times

    { n, x } — Matches the pattern from a minimum of n number of times to a maximum of x number of times

### OR Operator

The OR operator (|), makes it so the string being looked for is less accurate. You must be thinking: "Why make it LESS accurate?" Because having options is beneficial when looking for data.

For this example, we'll use: (abc):(123)

As is, the expression is ONLY looking for 'abc' and '123'. BUT with the or | operator, we can say (a|b|c):(1|2|3)

This makes it so 'abc' and '123' are accepted; but it will also take 'cab' and '321' since it's less specific.

### Character Classes

A character class in a regex defines a set of characters, any one of which can occur in an input string to fulfill a match. We've actually already discussed some character classes. The bracket expressions outlined previously, including positive and negative character groups, are considered character classes.

Here are some of the other common character classes:

.—Matches any character except the newline character (\n)

\d—Matches any Arabic numeral digit. This class is equivalent to the bracket expression [0-9].

\w—Matches any alphanumeric character from the basic Latin alphabet, including the underscore (_). This class is equivalent to the bracket expression [A-Za-z0-9_].

\s—Matches a single whitespace character, including tabs and line breaks

Each of the last three character classes can be changed to perform an inverse match by capitalizing the letter character. For example, \D matches a non-digit character.

### Flags

We started this tutorial by explaining that as a literal, a regex must be wrapped in slash characters. The one exception to this rule is with the component known as flags. Flags are placed at the end of a regex, after the second slash, and they define additional functionality or limits for the regex. There are six optional flags that can be used, either separately or together and in any order, but these are the three you're most likely to encounter:

g—Global search: the regex should be tested against all possible matches in a string.

i—Case-insensitive search: case should be ignored while attempting a match in a string

m—Multi-line search: a multi-line input string should be treated as multiple lines

### Grouping and Capturing

The “Matching a Username” regex is fairly straightforward and open-ended about what it accepts. As regular expressions grow more complicated, you may check multiple parts of a string to determine that different sections fulfill different requirements. To break these sections up, you'll need to use grouping constructs.

The primary way you group a section of a regex is by using parentheses (()). Each section within parentheses is known as a subexpression.

The following example contains two grouping constructs or subexpressions:

(abc):(xyz)
The first subexpression is looking for a part of the string that matches the string "abc" exactly. Similarly, the second subexpression is looking for "xyz". In between the subexpressions, we have a colon (:). Thus, the string "abc:xyz" would match, but the string "acb:xyz" would not. Unlike bracket expressions, subexpressions look for an exact match unless they're told to do otherwise.

Grouping constructs have two primary categories: capturing and non-capturing. The details about how capturing and non-capturing groups are used are beyond the scope of this tutorial. The important thing to understand is that capturing groups capture the matched character sequences for possible re-use (including a numbered backreference) while non-capturing groups do not. A grouping construct can be made non-capturing by adding the characters ?: at the beginning of an expression inside the parentheses.

### Bracket Expressions

Anything inside a set of square brackets ([]) represents a range of characters that we want to match. These patterns are known as bracket expressions, but they are also known as a positive character group, because they outline the characters we want to include. We can write these expressions to include all of the characters we want to match. For example, [abc] will look for a string that includes a or b or c, regardless of the length of the string. So all of the following examples would match: "aaa", "bin" "court", "abracadabra", and "bca".

You'll more commonly see a hyphen (-) used between alphanumeric characters (letters and numbers only) to represent a range of those possible characters. This means that [a-c] and [abc] will look for the exact same thing.

In our “Matching a Username” regex example, we can break down the bracket expressions as follows:

[a-z]—The string can contain any lowercase letter between a–z. Keep in mind that this looks for lowercase characters only. If we wanted to include uppercase characters, we would need to change the expression to [a-zA-Z].

[0-9]—The string can contain any number between 0–9

[_-]—The string can contain an underscore or hyphen. Both the underscore and the hyphen are called special characters. Special characters include any non-alphanumeric characters, such as punctuation or symbols. In this case, we only want a string that includes _ or -. It's important to note that the hyphen here is not the same hyphen that we used in our alphanumeric ranges. In bracket expressions, special characters that we want to include follow alphanumeric character ranges within the brackets.

If we put all of these expressions together so that our pattern is [a-z0-9_-], this will match any string that includes any combination of lowercase letters between a and z, any number between 0 and 9, and the special characters of an underscore or a hyphen. Keep in mind that these characters can be in any order. It's also important to note that this pattern does not require the string to meet all of these requirements; it can meet any of them.

The following examples fulfill the requirements of this regex:

"lernantino"

"lernantino1"

"l3rnantino_1"

"lern-antino"

"21452"

"_-_-"

What about the string "Lernantino"? This would not match our pattern because it includes an uppercase character, L.

It's important to note that a bracket expression can be turned into a negative character group by adding the ^ symbol to the beginning of the expression inside the brackets. A common example is matching a string that doesn't include any vowels. The pattern [^aeiouAEIOU] would find any strings that don't include lowercase or uppercase vowels.

### Greedy and Lazy Match

### Boundaries

### Back-references

### Look-ahead and Look-behind

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)