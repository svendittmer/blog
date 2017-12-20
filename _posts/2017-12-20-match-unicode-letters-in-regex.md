---
layout: post
title: 'TIL: Match unicode letters in regex'
date: 2017-12-20 11:47 +0100
---
Today I faced an interesting challenge on
[exercism.io](http://exercism.io).
To me, the most interesting part was about finding out if a sentence was
yelled or not. A sentence counts as yelled if all its word are upper
case.

You can find the whole challenge here:
[Bob in elixir - exercism.io](http://exercism.io/exercises/elixir/bob/readme)

Here's my first attempt:

```elixir
String.upcase(input) == input
```

This one passes some tests, but it failes for sentences that don't
contain any word, like "*1, 2, 3*". Since there's no upper case word,
it shouldn't count as yelled.
Next try:

```elixir
input =~ ~r/\w/u && String.upcase(input) == input
```

With this regex, I made sure the word contains at least on letter.
And since I'm still checking that every letter is upper case,
that should do the job, right? Well, not quite.

The exercise's last test was about a sentence yelled in Russian.
(Link:
[Bob in elixir test suite](http://exercism.io/exercises/elixir/bob/test-suite#L81))
Turns out `\w` matches only letters of the latin alphabet.
It is equivalent to `[a-zA-Z]`. To make the regex work,
I'd have to match any unicode letter. After googling a little bit,
I found the solutions here: [Regular-Expressions.info](https://www.regular-expressions.info/unicode.html).
In <abbr title="Perl Compatible Regular Expressions">PCRE</abbr> we can
match different categories of unicode with `\p{<some_unicode_category>}`.
For letters, you can use `\p{Letter}` or its short form `\p{L}`.
Here's the final code that makes the last test pass:

```elixir
input =~ ~r/[\p{L}]/u && String.upcase(input) == input
```
