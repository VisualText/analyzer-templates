# Bare Minimum

The smallest possible analyzer skeleton — no dictionary, no rules.

## Analyzer Notes

This is the most minimal analyzer template: a single `tokenize` pass that splits the input into a token list, with an empty knowledge base and no grammar rules. Nothing stands between you and a blank slate.

Use it when you want to build an analyzer entirely from scratch. Add passes to `spec/analyzer.seq`, write grammar and code files in `spec/`, and grow the knowledge base under `kb/` as your analyzer takes shape.

To run the analyzer, create a text file in the `input` folder (a sample is provided) and run it, then inspect the token list in the analyzer's output.
