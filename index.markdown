---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

Regular expressions are powerful and essential tools for programmers. In this guide, you'll find the basics of how to work with them, address performance issues and how to avoid them, and finally, best practices for writing your regular expressions.

**Note:** While the code examples are in JavaScript, the patterns and how they work are similar in most programming languages. Feel free to try them in your preferred language!

**See deployed page:** https://julian776.github.io/Regular-Expressions-Fast-as-Possible

# Table of Contents

- [Table of Contents](#table-of-contents)
- [Basics of Regular Expressions](#basics-of-regular-expressions)
- [Creating Patterns](#creating-patterns)
  - [Character Ranges](#character-ranges)
- [Modifiers](#modifiers)
  - [Asterisk `*`](#asterisk-)
  - [Plus `+`](#plus-)
  - [Curly Braces `{}`](#curly-braces-)
  - [Dot `.`](#dot-)
  - [Question Mark `?`](#question-mark-)
  - [Caret `^`](#caret-)
- [Creating Complex Patterns](#creating-complex-patterns)
  - [Understanding Expressions like `^[abety]`](#understanding-expressions-like-abety)
- [Performance](#performance)
  
# Basics of Regular Expressions

Regular expressions (regex) are used to match patterns in strings. You provide a pattern, and the regex compares it to the string you want to check. If the pattern matches, the regex returns true; otherwise, it returns false. Let's start with the fundamentals.

In JavaScript, there are two ways to create a regex:

```javascript
const regex = /regex-pattern-here/; // Using this syntax, you don't need quotes.
const regex = new RegExp("regex-pattern-here"); // The pattern is provided as a string.
```

# Creating Patterns

The most basic pattern is an exact match:

```javascript
const regex = /jhon/
const strToCheck = "jhon"

console.log(regex.test(strToCheck)) //Prints true
```

## Character Ranges

You can create a range in your pattern using [start-end]:

```javascript
const regex1 = /[0-9]/ //Match numbers from 0 to 9
const regex2 = /[2-5]/ //Match numbers from 2 to 5

const resultRegex1 = regex1.test("9") // true
const resultRegex2 = regex2.test("9") // false => The number 9 is not in range
```
You can specify a range of letters

**Note: Keep in mind that regex patterns are case-sensitive:**

```javascript
const regex1 = /[a-z]/ //Match any letter in lowercase
const regex2 = /[A-Z]/ //Match any letter in uppercase

const resultRegex1 = regex1.test("W") // false => The letter is upper case and the regex1 checks all letters lower case
const resultRegex2 = regex2.test("E") // true
```

To make our regex **case-insensitive**, we can add the letter 'i' at the end.
```javascript
const regex = /[a-z]/i //Match any letter case-insensitive

const resultRegex = regex.test("W") // true
```

# Modifiers

Modifiers add specificity to regex patterns. Let's explore what each modifier means.

## Asterisk `*`

The asterisk indicates that the preceding character can appear 0 or more times:

```javascript
const regex = /a*b/

const regexResult = regex.test("aaaaab") // true => The pattern matches b, ab, aab, aaab, ....aaaaaaaaaaaaaaaaaaab
```

## Plus `+`

The plus sign indicates that the preceding character must appear 1 or more times:

```javascript
const regex = /a*b/

const regexResult = regex.test("aaaaaaaaaaab") // true => The pattern matches ab, aab, aab, aaaab ... aaaaaaaaaaaaaaaaaaaaab
```
Keep in mind that some strings like "aabbb" will be false because the b is explicitly required only once.

## Curly Braces `{}`

Curly braces specify a range of times a character can appear in a string:

```javascript
const regex1 = /a{0,2}b/; // Matches b, ab, aab
const regex2 = /a{1,}b/; // Matches ab, aab, aaab, ...
const regex3 = /a{2}b/; // Matches aab only
```

## Dot `.`

The dot is a wildcard that matches any character:

```javascript
const regex = /ab./; // Matches ab*, ab!, abr, ab4, ...
```

## Question Mark `?`

The question mark indicates that the preceding character can appear 0 or 1 time:

```javascript
const regex1 = /a?b/; // Matches b, ab
const regex2 = /a*?b/; // Matches b, ab
```

## Caret `^`

The caret has two roles: it can match a character at the start of a string or negate a character:

```javascript
const regex1 = /^ab/; // Matches ab at the start of the string
const regex2 = /[^ab]/; // Matches any character except a or b
const regex3 = /^[abrt]/; // Matches a, b, r, or t at the start of the string
```

We introduce a different way to use \[\], just wait a second.

# Creating Complex Patterns

To create complex patterns, you can mix modifiers, ranges, and more in the same pattern. The order in which your pattern is written is the order in which the string must match it. For example, to validate a number at the start of a string, followed by a lowercase letter, and ending with "#," the pattern would be /[0-9][a-z]#/.

Remember that you can configure your pattern to suit your specific string validation needs.

## Understanding Expressions like `^[abety]`

Expressions like this mean that the caret ^ affects all characters within the brackets []. If you want to match those characters exactly at the beginning of a string, you can create a pattern like /abety[0-9]/.

```javascript
const regex1 = /^[abety]/; // Matches a, b, e, t, y, or more complex strings
const regex2 = /[0-9]+/; // Matches any digit one or more times
const regex3 = /[^a-zA-Z]/; // Matches any character except letters
```

# Performance

It is always preferred to make your regex fail quickly to save computation time and enhance program efficiency.

This concept can save you a significant amount of time when querying databases. For instance, if you're searching for a phone number and you only have the initial digits, you can:

```javascript
const regex = /17895/ // Matches 17895 in any part of fthe string
```

In the regex above, you have a query that searches the database but checks for a match anywhere in the strings. Later, you can refine your query to make the regex search only for the specific substring it contains at the beginning.

```javascript
const regex = /^17895/ // Matches 17895 at the beginning of the string
```

Please note that the regex will fail immediately if the first characters do not match, eliminating the need to evaluate the entire string for a match.
