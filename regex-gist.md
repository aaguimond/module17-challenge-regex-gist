# Regular Expression Phrase Brief

Explaning a regex phrase


## Summary

The following regular expression (regex) validates hexidecimal codes.

```
/^#?([a-f0-9]{6}|[a-f0-9]{3})$/
```

This would be commonly used to check that color codes are have correct syntax. It works for both hex codes that start with a "#" and those that don't, as well as for either 6-digit or 3-digit hex codes.


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

As stated above in [bracket expressions](#bracket-expressions), character classes are related to bracket expressions in regex. Character classes will be the letters and numbers within our [grouping constructs](#grouping-constructs).

<pre><code>
/^#?([<span style="color:yellow">a-f</span><span style="color:red">0-9</span>]{6}|[<span style="color:yellow">a-f</span><span style="color:red">0-9</span>]{3}$/
</code></pre>

___

### The OR Operator


___

### Flags


___

### Character Escapes


___

## Author

Please reach out to me with any questions:

- Github: [aaguimond](https://github.com/aaguimond)
- Email: aidanguimond2024@u.northwestern.edu