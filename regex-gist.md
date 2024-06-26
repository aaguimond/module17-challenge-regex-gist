# Regular Expression Phrase Brief

Explaining a regex phrase


## Summary

The following regular expression (regex) validates hexadecimal codes.

```
/^#?([a-f0-9]{6}|[a-f0-9]{3})$/
```

This would be commonly used to check that color codes have correct syntax. It works for both hex codes that start with a "#" and those that don't, as well as for either 6-digit or 3-digit hex codes.


## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)


## Regex Components

Regular expressions may appear to be random characters to new developers, but they are finely structured snippets that tell the code what structure they should expect for values given to them. Regex are made up of [anchors](#anchors), [quantifiers](#quantifiers), [grouping construct(s)](#grouping-constructs), [bracket expression(s)](#bracket-expressions), [character class(es)](#character-classes), [flag(s)](#flags), [character escape(s)](#character-escapes), and possibly an [or operator](#the-or-operator). The regex phrase covered in this gist contains all of the above elements excluding flags and character escapes.
___

### Anchors

The anchors in regex are the symbols that denote the beginning and ending of complex phrases. The `^` character is the start anchor and the `$` is the end anchor. These anchors allow us to be specific about what hexadecimal codes we want to verify. The anchors in our regex are highlighted below.

<pre><code>
/<span style="color:yellow">^</span>#?([a-f0-9]{6}|[a-f0-9]{3})<span style="color:yellow">$</span>/
</code></pre>

Our start anchor, `^`, states that the string being verified must match our regex phrase from the very beginning.

Our start anchor, `$`, states that the string being verified must match our regex phrase until the very end.

Anchors are not required to make valid regex. In our use case, the strict requirement that we've made with our anchors enables us to correctly verify hexadecimal codes.
___

### Quantifiers

Quantifiers are operators that state how many occurrences of certain [characters](#character-classes) may appear in our regex. Our [regex phrase](#summary) uses three quantifiers:

* `?` - This quantifier states that the string we're verifying may include zero or one `#`. When combined with our anchors, this quantifier denotes that a valid hexadecimal code may or may not begin with a `#`.

* `{6}` - This quantifier states that there may only be exactly six of the element directly preceeding it. Since that element is written between `[]`, this quantifier allows any six of the elements included within that [character class](#character-classes).

* `{3}` - Similar to the above, this quantifier states that there may only be exactly three of the characters within the allowed scope.

The quantifiers in our example regex are highlighted in blue and the elements that they're acting upon are highlighted in green.

<pre><code>
/^<span style="color:lightgreen">#</span><span style="color:blue">?</span>(<span style="color:lightgreen">[a-f0-9]</span><span style="color:blue">{6}</span>|<span style="color:lightgreen">[a-f0-9]</span><span style="color:blue">{3}</span>)$/
</code></pre>
___

### Grouping Constructs

Grouping constructs are accomplished in regex with the use of `()` parentheses. Like in mathematics, grouping constructs allow us to treat patterns of code as a single entity. Our [regex phrase](#summary) uses a grouping construct that is necessary for our code to effectively verify all types of hexadecimal codes. The grouping construct in our example regex and the code it's acting upon are highlighted below.

<pre><code>
/^#?<span style="color:red">(</span><span style="color:lightpink">[a-f0-9]{6}|[a-f0-9]{3}</span><span style="color:red">)</span>$/
</code></pre>

In the case of our regex, all of the code between the `()` parentheses will be treated as the benchmark that we'll compare our to-be-verified hexadecimal codes to. Regex grouping constructs can also cover repeating phrases (like 123123123123...) by including a `+` at the end of the parentheses like so:

```
(123)+
```

This would match a string of "123", "123123", "123123123", and any other that contains that complete phrase in repetition.
___

### Bracket Expressions

Bracket expressions are closely linked to [character classes](#character-classes). A bracket expression will always contain one or more character classes that we use in our regex to match characters within the numbers or strings that we plan to verify. Bracket expressions are also similar to [grouping constructs](#grouping-constructs) in that they will group together pieces of regex code to create a logical component for us to accomplish the goal of our regex. They are practiced with `[]` square brackets. The bracket expressions and the code that they're acting upon are highlighted below.

<pre><code>
/^#?(<span style="color:blue">[</span><span style="color:orange">a-f0-9</span><span style="color:blue">]</span><span style="color:orange">{6}</span>|<span style="color:blue">[</span><span style="color:orange">a-f0-9</span><span style="color:blue">]</span><span style="color:orange">{3}</span>)$/
</code></pre>

As you can see, the bracket expression includes everything within the `[]` square brackets, but also the [quantifiers](#quantifiers) to the right of the brackets. This is due to the fact that the quantifiers are acting upon the [character classes](#character-classes) within the brackets, and as such are part of the logic of the bracket expression. It may be helpful to think of bracket expressions as smaller functional parts within a larger regex phrase.
___

### Character Classes

As stated above in [bracket expressions](#bracket-expressions), character classes are related to bracket expressions in regex. Character classes will be the characters (the letters and numbers) within our [grouping constructs](#grouping-constructs). Character classes are used to define what the allowed characters are for the string that our regex will verify. Character classes are usually written as ranges of characters with a beginning character for the start of the range, a `-` dash, and an ending character for the end of the range. Ranges can also be combined, as in our [example regex phrase](#summary). Our example contains ranges of letters from `a` through `f`, as well as numbers `0` through `9`. These character classes are highlighted in the code below.

<pre><code>
/^#?([<span style="color:yellow">a-f</span><span style="color:red">0-9</span>]{6}|[<span style="color:yellow">a-f</span><span style="color:red">0-9</span>]{3}$/
</code></pre>

The reason that we want numbers `0-9` AND letters `a-f` in our regex is because hexadecimal notation uses base-16 counting. By contrast, we use base-10 in our non-coding mathematics, meaning that we have 10 unique digits and another order of magnitude is created after `9` (eg 99 => 100). Base-16 must use other single characters (`a-f`) to fill in as representations of 10, 11, 12, 13, 14, and 15 since base-16 counting will only increase another order of magnitude after `15`. As such, we want our regex to only allow the characters of `0` through `9` and `a` through `f`.

We can count to 47 using hexadecimal with our hexadecimal base-16 numbers and their corresponding base-10 values in the table below.

| Hexadecimal (base-16) | Base-10 | Hexadecimal (base-16) | Base-10 | Hexadecimal (base-16) | Base-10 |
| --------------------- | ------- | --------------------- | ------- | --------------------- | ------- |
| 0 | 0 | 10 | 16 | 20 | 32 |
| 1 | 1 | 11 | 17 | 21 | 33 |
| 2 | 2 | 12 | 18 | 22 | 34 |
| 3 | 3 | 13 | 19 | 23 | 35 |
| 4 | 4 | 14 | 20 | 24 | 36 |
| 5 | 5 | 15 | 21 | 25 | 37 |
| 6 | 6 | 16 | 22 | 26 | 38 |
| 7 | 7 | 17 | 23 | 27 | 39 |
| 8 | 8 | 18 | 24 | 28 | 40 |
| 9 | 9 | 19 | 25 | 29 | 41 |
| a | 10 | 1a | 26 | 2a | 42 |
| b | 11 | 1b | 27 | 2b | 43 |
| c | 12 | 1c | 28 | 2c | 44 |
| d | 13 | 1d | 29 | 2d | 45 |
| e | 14 | 1e | 30 | 2e | 46 |
| f | 15 | 1f | 31 | 2f | 47 |
___

### The OR Operator

The OR operator `|` is used similarly to how it's used in Javascript. When using it, we want to place two conditions, or in the case of our [example regex](#summary) phrase [bracket expressions](#bracket-expressions), on either side of the `|` OR operator. This tells the code that we will accept either of the conditions on the right or left of it as valid. The OR operator is highlighted in the code below.

<pre><code>
/^#?([a-f0-9]{6}<span style="color:green">|</span>[a-f0-9]{3})$/
</code></pre>

In the case of our regex example, we're saying that either

```
[a-f0-9]{6}
```

_OR_

```
[a-f0-9]{3}
```

are valid, verified hexadecimal codes.

___

### Conclusion

When we put _all_ of the above parts together, we can easily understand our [example regex phrase](#summary)

```
/^#?([a-f0-9]{6}|[a-f0-9]{3})$/
```

We have our [anchors at the beginning and end](#anchors) that tells our code where the regex starts and finishes:

<pre><code>
/<span style="color:red">^</span>#?([a-f0-9]{6}|[a-f0-9]{3})<span style="color:red">$</span>/
</code></pre>

We have our first [quantifier](#quantifiers) stating that either zero or one `#` is allowed:

<pre><code>
/^<span style="color:pink">#</span><span style="color:red">?</span>([a-f0-9]{6}|[a-f0-9]{3})$/
</code></pre>

We have our [grouping construct](#grouping-constructs) that states what the allowed characters are:
<pre><code>
/^#?<span style="color:red">(</span><span style="color:lightpink">[a-f0-9]{6}|[a-f0-9]{3}</span><span style="color:red">)</span>$/
</code></pre>

We have our [bracket expressions](#bracket-expressions):

<pre><code>
/^#?(<span style="color:red">[</span><span style="color:pink">a-f0-9</span><span style="color:red">]</span><span style="color:pink">{6}</span>|<span style="color:red">[</span><span style="color:pink">a-f0-9</span><span style="color:red">]</span><span style="color:pink">{3}</span>)$/
</code></pre>

That contain our [character classes](#character-classes) in <span style="color:red">red</span> and their [quantifiers](#quantifiers) in <span style="color:orange">orange</span>:

<pre><code>
/^#?(<span style="color:pink">[</span><span style="color:red">a-f0-9</span><span style="color:pink">]</span><span style="color:orange">{6}</span>|<span style="color:pink">[</span><span style="color:red">a-f0-9</span><span style="color:pink">]</span><span style="color:orange">{3}</span>)$/
</code></pre>

And we have our [OR operator](#the-or-operator):

<pre><code>
/^#?([a-f0-9]{6}<span style="color:red">|</span>[a-f0-9]{3})$/
</code></pre>

When we put them all together, our regex is saying that we will validate hexadecimal codes and hex codes that _can_ contain `#` only at the beginning and then have either 3 _or_ 6 characters that can only be the digits `0` through `9` and the letters `a` through `f`.

How awesome is that!
___

## Author

Please reach out to me with any questions:

- Github: [aaguimond](https://github.com/aaguimond)
- Email: aidanguimond2024@u.northwestern.edu