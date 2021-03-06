<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

**Table of Contents**

- [Regex Workshop](#regex-workshop)
  - [Introduction](#introduction)
    - [Definitions of regular expressions](#definitions-of-regular-expressions)
    - [Basic concepts](#basic-concepts)
  - [In reality - programming languages!](#in-reality---programming-languages)
  - [More References](#more-references)
  - [Lessons](#lessons)
    - [Lesson 1 - Warming up!](#lesson-1---warming-up)
    - [Lesson 2 - Regex in javascript JavaScript wild.](#lesson-2---regex-in-javascript-javascript-wild)
    - [Lesson 3 - Now we are experts! Let’s try some challenges.](#lesson-3---now-we-are-experts-let%E2%80%99s-try-some-challenges)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Regex Workshop
Let's start Regular expressions workshop!

**Requirements:** Git client, Browser, Editor (with JavaScript support) and your courage.

## Introduction

>   :alien: What the h*ll is this:

```
/^([a-zA-Z0-9._%+-]+@(?:[a-zA-Z0-9-]+\.)+[a-zA-Z]{2,4})(, ?([a-zA-Z0-9._%+-]+@(?:[a-zA-Z0-9-]+\.)+[a-zA-Z]{2,4}))*?$/
```

> Or this?

```
/^([A-PR-UWYZ0-9][A-HK-Y0-9][AEHMNPRTVXY0-9]?[ABEHMNPRVWXY0-9]? {1,2}[0-9][ABD-HJLN-UW-Z]{2}|GIR 0AA)$/
```

> But that’s easy – right?

```
/^([0-9]{5}(-[0-9]{4})?|[A-Z]\d[A-Z]((\s|\-)?\d[A-Z]\d)?)$/i
```

> Really?   :joy:

```
/^\/\^?([^\/]|\\\/)+\$?\/([gimsx]{0,5})?$/
```

> “ Those are regular expressions. Regular expressions are our friends. They’re neither evil nor do they hurt humans. They require good care, occasional petting and a bit of grooming – but are easy to deal with besides that. ”

Quite a few people have some sort of a rough idea what regular expressions do, what they’re useful for and why really every developer should at least have an idea of using RegExps (as care-takers call them). For web developers **regular expressions could be used everywhere**:
- form field data validation (either on the client with JavaScript or Flash/Flex or on pretty much any backend from CF via PHP to Java or Ruby)
- text pattern recognition
- URL rewrite rules with Apache or IIS
- powerful replace feature in you text editors
- and many more.

### Definitions of regular expressions

**Regular expressions are patterns used to match character combinations in strings.**

Regular expression (abbreviated regex or regexp) is a **sequence of characters** that define a search pattern, mainly for use in pattern matching with strings, or string matching, i.e. "find and replace"-like operations. The concept arose in the 1950s, when the American mathematician Stephen Kleene formalized the description of a regular language, and came into common use with the Unix text processing utilities ed, an editor, and grep (global regular expression print), a filter.

Regular expressions are so useful in computing that the various systems to specify regular expressions have evolved to provide both a basic and extended standard for the grammar and syntax; modern regular expressions heavily augment the standard. Regular expression processors are found in several search engines, search and replace dialogs of several word processors and text editors, and in the command lines of text processing utilities, such as sed and AWK.

Many programming languages provide regular expression capabilities, some built-in, for example Perl, JavaScript, Ruby, AWK, and Tcl, and others via a standard library, for example .NET languages, Java, Python and C++ (since C++11). Most other languages offer regular expressions via a library.

 :exclamation: **PATTERN**

Each character in a regular expression is either understood to be a **metacharacter** with its special meaning, or a **regular character** with its literal meaning. Together, they can be used to identify textual material of a given pattern, or process a number of instances of it that can vary from a precise equality to a very general similarity of the pattern.

### Basic concepts

**Boolean "or"**

A vertical bar separates alternatives. For example, gray|grey can match "gray" or "grey".

**Grouping**

Parentheses "()" are used to define the scope and precedence of the operators (among other uses). For example, ```gray|grey``` and ```gr(a|e)y``` are equivalent patterns which both describe the set of "gray" or "grey".

**Quantification**

A quantifier after a token (such as a character) or group specifies how often that preceding element is allowed to occur. The most common quantifiers are:


- ```?``` The question mark indicates there is zero or one of the preceding element. For example, ```colou?r``` matches both "color" and "colour".
- ```*``` The asterisk indicates there is zero or more of the preceding element. For example, ```ab*c``` matches "ac", "abc", "abbc", "abbbc", and so on.
- ```+``` The plus sign indicates there is one or more of the preceding element. For example, ```ab+c``` matches "abc", "abbc", "abbbc", and so on, but not "ac".

More advanced concepts (https://en.wikipedia.org/wiki/Regular_expression)

| MetaChar     | Meaning     |
| :------------- | :------------- |
| ```.```   | Matches any single character (many applications exclude newlines, and exactly which characters are considered newlines is flavor-, character-encoding-, and platform-specific, but it is safe to assume that the line feed character is included). Within POSIX bracket expressions, the dot character matches a literal dot. For example, ```a.c``` matches "abc", etc., but ```[a.c]``` matches only "a", ".", or "c".       |
| ``[]``    | A bracket expression. Matches a single character that is contained within the brackets. For example, ```[abc]``` matches "a", "b", or "c". ```[a-z]``` specifies a range which matches any lowercase letter from "a" to "z". These forms can be mixed: ```[abcx-z]``` matches "a", "b", "c", "x", "y", or "z", as does ```[a-cx-z]```. <br>*The - character is treated as a literal character if it is the last or the first (after the ^, if present) character within the brackets:* ```[abc-]```, ```[-abc]```. *Note that backslash escapes are not allowed. The ] character can be included in a bracket expression if it is the first (after the ^) character:* ```[]abc].``` |
| ```[^ ]```  | Matches a single character that is not contained within the brackets. For example, ```[^abc]``` matches any character other than "a", "b", or "c". ```[^a-z]``` matches any single character that is not a lowercase letter from "a" to "z". Likewise, literal characters and ranges can be mixed. |
| ```^```   | Matches the starting position within the string. In line-based tools, it matches the starting position of any line. |
| ```$```   | Matches the ending position of the string or the position just before a string-ending newline. In line-based tools, it matches the ending position of any line. |
| ```( )``` | Defines a marked subexpression. The string matched within the parentheses can be recalled later (see the next entry, \n). A marked subexpression is also called a block or capturing group. |
| ```\n``` | Matches what the nth marked subexpression matched, where n is a digit from 1 to 9. This construct is vaguely defined in the POSIX.2 standard. Some tools allow referencing more than nine capturing groups. |
| ```*```| Matches the preceding element zero or more times. For example, <br>```ab*c``` matches "ac", "abc", "abbbc", etc. <br>```[xyz]*``` matches "", "x", "y", "z", "zx", "zyx", "xyzzy", and so on.<br> ```(ab)*``` matches "", "ab", "abab", "ababab", and so on. |
| ```{m,n}``` | Matches the preceding element at least m and not more than n times. For example, ```a{3,5}``` matches only "aaa", "aaaa", and "aaaaa". |

Escaping of special characters is done by backslash, eg. “\(in bracket\)”.

| MetaChar     | Meaning     |
| :------------- | :------------- |
|```\b``` | Matches a zero-width boundary between a word-class character (see next) and either a non-word class character or an edge. |
|```\w``` | Matches an alphanumeric character, including "_";  Alternative regular is ```[A-Za-z0-9_]``` |
|```\W``` | Matches a non-alphanumeric character, excluding "_"; Alternative regular is  ```[^A-Za-z0-9_]``` |
|```\s``` | Matches a whitespace character, which in ASCII are tab, line feed, form feed, carriage return, and space; in Unicode, also matches no-break spaces, next line, and the variable-width spaces (amongst others). |
|```\S``` | Matches anything BUT a whitespace. |
|```\d``` | Matches a digit; same as ```[0-9]``` |
|```\D``` | Matches a non-digit; same as ```[^0-9]``` |
|```\t \n \r``` | tab, linefeed, carriage return |
|... |...|
|```\u00A9``` | Unicode characters can be escaped like this |
|```(?:abc)``` | non-capturing group |
|```(?=abc)``` | positive lookahead |
|```(?!abc)``` | negative lookahead |
|```a+? a{2,}?``` | match as few as possible |

## In reality - programming languages!

**JavaScript**

Ref: http://www.w3schools.com/js/js_regexp.asp

In JavaScript, regular expressions are also objects. These patterns are used with the exec and test methods of RegExp, and with the **match**, **replace**, **search**, and **split** methods of String.
```javascript
var str = "Visit W3Schools";
var n = str.search(/w3schools/i);
// n = 6 -> matches at 6 character of input
```

**Freemarker (gearbox)**

Ref: http://freemarker.org/docs/ref_builtins_string.html
Uses java regular expressions - http://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html

Method: **matches**

http://freemarker.org/docs/ref_builtins_string.html#ref_builtin_matches

```
<#if "foo bar fyo"?matches("f.?o")>
    <#-- it matches! -->
</#if>
```

If the regular expression contains groups (parentheses), then you can access them with the groups built-in:

```
<#-- Entire input match -->
<#assign res = "Juraj Husar"?matches(r"(\w+) (\w+)")>
<#if res> <#-- We can't try to access groups if there was no match! -->
  First name: ${res?groups[1]}
  Second name: ${res?groups[2]}
</#if>
```

Method: **replace** - should also allow regex support

we need to specify third parameter to allow regex replacing

http://freemarker.org/docs/ref_builtins_string.html#ref_builtin_string_flags

```
${someText?replace('ba*', 'XY', 'ri')}
```

## More References

Wiki Regex
- https://en.wikipedia.org/wiki/Regular_expression

JavaScript
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions

Regex Tester
- https://regex101.com
- http://regexr.com/

## Lessons

Now let's try write some regular expressions!

### Lesson 1 - Warming up!

If you want, you can use https://regex101.com/ as helper for more detailed testing and information about your pattern.

Open `lesson1/index.html` and finish first lesson.

### Lesson 2 - Regex in javascript JavaScript wild.

The purpose of this task is to supplement the code several functions (you can find them in `lesson2/script.js`).<br>
You can see track progress here `lesson2/index.html`.<br>
Your job is to fill the missing regular expressions (in the shortest possible form) so that the following conditions are met:

1. **verifyNumber** function checks if input is number from 2 up to 5 digits.

3. **verifyImageName** function checks if the file name is entered in correct form.
(Name may contain only small, large letters, digits, and _ and the  extension `png` or `jpg`).

4. **verifyName** function checks whether the user has correctly entered specific names and (optional!) surname. The name should begin with the `Ju` or `Ma` letters, followed by a maximum of five lowercase letters. Optional surname should begin with a capital letter and contain up to 9 letters.
First and last name separated by a single space (unless the user specifies surname).
Eg. `Juraj Milanovic`, or `Martin`.

5. **verifyPassword** function checks whether the user has entered the password correctly. The password should contain at least one lowercase letter, at least one uppercase letter
and at least one number. The password should be at least five characters (allowed characters are: `digits`, `uppercase` and `lowercase` letters and `@`, `%`, `$`, `*`)<br>
*Hint: positive lookahead*

5. **doMath** function is mathematical example. We have two numbers and sign which determine mathematical operation. Example `1 + 3`, `77 / 11` etc. Function should return result (eg. sum of 2 number). This should be helpfull http://www.w3schools.com/jsref/jsref_obj_regexp.asp.

6. **doRearangement** function is special function which gets Adress from input text and format it like `State, City Zip`. Input is `Name [Surname], State, Zip City`. Name and City is composed from letters and Zip is number. In this example there is no need to handle extreme cases.<br>
Example input: `Alexander, 15 Bratislava, Slovakia`<br>
Example output: `Slovakia, Bratislava, 15`<br>
*Hint: $1*

7. **stripHtmlTags** function should strip HTML tags and return only plain text. For example for input `<a href="#">TEXT</a>` should be returned only `TEXT`. If you remove all tags like `<item>`, `</item>`, `<item />`, you should match all test cases.<br>
*Hint: modifiers*

### Lesson 3 - Now we are experts! Let’s try some challenges.

We can play a little. :sunglasses:
Open http://regex.alf.nu/ and start game!

Some levels are really hardcore, so don't be shy and skip some of them. But try to do as many as you can.

**Tell me your final score!** :)

Another interesting regular expressions "game" is http://regexcrossword.com/.

If you don't have enough then try http://regexone.com/.

And don't remember to finish academy https://www.codecademy.com/courses/javascript-intermediate-en-NJ7Lr/0/1.

*That's all folks.*
