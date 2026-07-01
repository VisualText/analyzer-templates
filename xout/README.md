# XOUT

An analyzer that masks alphanumeric text as "x"

## Analyzer Notes

This is an NLP++ Analyzer that redacts text by replacing every alphanumeric word with a run of `x` characters while leaving the overall structure intact. It is useful for sanitizing sample documents (for example the resumes in `input/Resumes`) so they can be shared or inspected without exposing the real content: line breaks, spacing, punctuation, and the length and capitalization pattern of each word are all preserved.

Each letter or digit is replaced one-for-one, so a masked word is the same length as the original. Uppercase letters become `X` and everything else becomes `x`, which keeps the capitalization pattern visible.

For example, the input line:

```
Data Engineering Analyst
```

is masked to:

```
Xxxx Xxxxxxxxxxx Xxxxxxx
```

Punctuation, numbers-as-length, and whitespace stay in place, so the shape of the document is faithfully reproduced while the words themselves are hidden.

To run the analyzer, create a text file in the input folder consisting of the text to be redacted. The masked result for each file is written to a mirror file under `input/X/`.
