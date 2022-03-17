# Regexs Fast as possible

Regexs are powerfull and one important tool as a programmer.
Here you will find basics of how to work with them, some performance problems and how to avoid them and finally good practices writing your regexs.

### Code examples will be in JavaScript but regexs patterns and how they work is the same in most languages
### Try in your preferred language!

# Basic of regexs

Regex basically match patterns. We have to tell the pattern and the regex will compare the pattern with some string we want.
If the pattern corresponds regex returns true if not returns false. (Regex can do more than return true or false but first the basics)

In JS we have two ways to write a regex

```Javascript
const regex = /regex-pattern-here/ //With this syntax you not use string
const regex = new RegExp("regex-pattern-here") //The pattern is given as a string
```

## We have the syntaxs but how we create a pattern?

### The most basic pattern we can create is an exact match

```Javascript
const regex = /tatiana/
const strToCheck = "tatiana"

console.log(regex.test(strToCheck)) //Prints true
```

### Range

We create a range in our pattern with **\[start-finall\]**

```Javascript
const regex1 = /[0-9]/ //Match numbers from 0 to 9
const regex2 = /[2-5]/ //Match numbers from 2 to 5

const resultRegex1 = regex1.test("9") // true
const resultRegex2 = regex2.test("9") // false => The number 9 is not in range
```
You can specify a range of letters
**Note: Regexs pattern are sensitive to upper case and lower case letters. Take in mind**

```Javascript
const regex1 = /[a-z]/ //Match any letter in lowercase
const regex = /[A-Z]/ //Match any letter in uppercase

const resultRegex1 = regex1.test("W") // false => The letter is upper case and the regex1 checks all letters lower case
const resultRegex2 = regex2.test("E") // true
```

## Modifiers

The modifiers allowed us to add specificity to our patterns. Lets look what each of them means in our patterns

### Asterisk *

The asterik tell that the preceding character can be 0 or more times.

```Javascript
const regex = /a*b/

const regexResult = regex.test("aaaaab") // true => The pattern matches b, ab, aab, aaab, .... aaaaaaaaaaaaaaaaaaab
```

### Sum symbol +

The  + tells that the preceding character can be 1 or more times

```Javascript
const regex = /a*b/

const regexResult = regex.test("aaaaaaaaaaab") // true => The pattern matches ab, aab, aab, aaaab ... aaaaaaaaaaaaaaaaaaaaab
```
You need to take in mind that some string like "aabbb" will be false because the b is explicitly one time and has no modifiers.

Another expression like "aaaa" will fail again because the pattern needs a b explictly.

### The {}

The {} tells to the pattern a range of times a character can exist in a strign.

```Javascript
const regex = /a{0, 2}b/ // Will match b, ab, aab
const regex = /a{,2}b/ //Will match b, ab, aab
const regex = /a{1,}b/ //Will match ab, aab, aaab, aaaaaaaab .... aaaaaaaaaaaaaaaaaaaaab ...
const regex = /a{2}b/ //Will match aab only
```

### The point .

This modifier is like a wildcard, where the point is can be any symbol.

```Javascript
const regex = /ab./ // Will match ab*, ab!, abr, ab4 ... and so on
```

### Question mark ?

The preceding character can be 0 or 1 time.

If you use the ? after any other modifier will make it non-greedy and matching only 0 or 1 times

```Javascript
const regex = /a?b/ //Will match b, ab
const regex = /a*?b/ //Will match b, ab
```

### ^

This modifier has two roles, look for some character at start of string or tells that not match.  
