# Bare English

A bare-minimum parser bundled with the full English dictionary.

## Analyzer Notes

This template is an otherwise-empty analyzer wired to the full English dictionary (`kb/user/en-full.dict`). It has no grammar rules of its own — the single `dicttokz` pass tokenizes the input and looks each token up in the dictionary, attaching part-of-speech and other dictionary attributes to the tokens.

It is a good starting point when you need dictionary lookup (word categories, known vocabulary) but don't want any domain-specific grammar pre-wired. Add your own passes to `spec/analyzer.seq` and grammar files to `spec/` to build on top of the tokenized, dictionary-tagged text.

To run the analyzer, create a text file in the `input` folder (a sample sentence is provided) and run it, then inspect the tokenized text tree in the analyzer's output.
