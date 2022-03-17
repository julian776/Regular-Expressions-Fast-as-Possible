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

# We have the syntaxs but how we create a pattern?

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
