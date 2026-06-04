# Analyzer Templates

These are template analyzers that appear in the **New Analyzer** selection list of the [NLP++ Language Extension for VSCode](https://marketplace.visualstudio.com/items?itemName=dehilster.nlp). When a user creates a new analyzer from the extension, they can pick one of these templates as a starting point and then extend it for their own domain.

For more on the NLP++ language and tooling, see the [VisualText / NLP++ project site](http://vscode.visualtext.org).

## Available Templates

Each folder in this repository is a self-contained analyzer template with its own `README.md`, sample `input/`, knowledge base (`kb/`), grammar/passes (`spec/`), and working directory (`tmp/`).

### [Address Parser](Address%20Parser/README.md)
A parser for American (USPS-format) postal addresses. Extracts house number, street name and suffix/type, city, state, ZIP code, and address type. Also handles Rural Route and Highway Contract addresses, exposing the extracted fields as JSON.

### [Bare English](Bare%20English/README.md)
A bare-minimum parser bundled with the full English dictionary. A good starting point when you need dictionary lookup but don't want any domain-specific grammar pre-wired.

### [Bare Minimum](Bare%20Minimum/README.md)
The smallest possible analyzer skeleton — no dictionary, no rules. Use this when you want to build an analyzer from scratch with nothing in the way.

### [Date and Times](Date%20and%20Times/README.md)
A date and time analyzer that recognizes common date and time expressions in text.

### [Email Addresses](Email%20Addresses/README.md)
Identifies email addresses across a variety of formats. For each match it extracts the local name, domain name, and top-level domain (TLD), and emits the result as JSON.

### [Paragraphs Sentences](Paragraphs%20Sentences/README.md)
Lays out the basics of paragraph and sentence segmentation with dictionary lookup. Intended as a starting point — each domain has its own quirks (abbreviations, lists, etc.) that can fool sentence enders and will need domain-specific handling.

### [Telephone Numbers](Telephone%20Numbers/README.md)
Recognizes telephone numbers in many international and US formats (e.g. `212.456.7890`, `+1 212-456-7890`, `1-212-456-7890`). For each number it extracts the area code, prefix, station, and phone type (mobile/landline).

### [URLs](URLs/README.md)
Identifies hyperlinks of many shapes and extracts the scheme (http/https/ftp/…), sub-domain, domain name, page path, and top-level domain, emitting the result as JSON.

### [XOUT](xout/README.md)
A utility analyzer that masks all alphanumeric text as `x`. Useful for sanitizing or redacting sample text while preserving structure.

## Using a Template

1. Install the [NLP++ Language Extension](https://marketplace.visualstudio.com/items?itemName=dehilster.nlp) in VSCode.
2. Create a new analyzer from the extension and choose one of the templates above.
3. Drop the text you want to parse into the analyzer's `input/` folder and run the analyzer.
4. Inspect the generated output (e.g. `input/<file>.txt_log/output.json`) and extend the rules in `spec/` and the knowledge base in `kb/` for your domain.

## Rules for Contributing a Template

These are the rules for submitting a block analyzer to this repository:

1. The folder name should be a two-to-three-word descriptive name for the analyzer.
2. The first line in the README should be the same title with a `#` header.
3. The next non-empty line should be a short description of the analyzer — this text appears in the NLP++ VSCode Extension's template selection list.
4. The rest of the README should explain how to use and extend the analyzer.

Example:

```
# Moose Analyzer

Allows for analyzing text for articles on moose (appears in the description of the selection block analyzer selection list)

## Using the Moose Analyzer

The way in which to best utilize this analyzer is...
```

## Cross-repo release automation

This repo participates in the VisualText cross-repo release "percolation"
system: submodule bumps flow downstream automatically via `repository_dispatch`.
See **[nlp-engine/docs/PERCOLATION.md](https://github.com/VisualText/nlp-engine/blob/master/docs/PERCOLATION.md)** for the full map.
