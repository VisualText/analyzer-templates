# Paragraphs Sentences

An analyzer that segments text into paragraphs and sentences

## Analyzer Notes

This is an NLP++ Analyzer that reads plain text and breaks it into paragraphs and sentences using dictionary token lookup. Sample articles can be found in the input folder (for example, input/article_01.txt).

The analyzer works in stages:

- Raw tokens are gathered into lines, and consecutive lines are grouped into paragraphs. A blank line separates one paragraph from the next.

- Inside each paragraph, terminal punctuation (`.`, `?`, `!`) followed by whitespace or the end of text marks the end of a sentence. Everything up to and including that boundary becomes a `_sentence` node.

For example, a paragraph such as:

> Four additional members of the gang have been charged today. According to the indictment, the gang originated in Chicago.

is split into two sentences at the period after "today".

Sentence segmentation has domain-specific quirks: some text looks like a sentence ender but is not. To handle this, earlier passes protect misleading periods before the sentence-ender pass runs:

- `abbreviations` groups dotted abbreviations like "U.S." so their interior periods are not treated as sentence boundaries.

- `initials` groups a middle initial and its period (as in "John R. Jones") for the same reason.

Each domain will be different, so you will need to look for the specific text that would fool the sentence enders and protect it in the same way.

To run the analyzer, create a text file in the input folder consisting of the text to be parsed.
