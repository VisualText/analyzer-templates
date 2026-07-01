# Telephone Numbers

An analyzer for telephone numbers

## Analyzer Notes

This is an NLP++ Analyzer that parses through text and identifies Telephone numbers listed in the text. Some sample telephone number formats can be found in input/text.txt

Here are some examples
- 212.456.7890
- 212 456 7890
- +12124567890
- +12124567890
- +1 212.456.7890
- +212-456-7890
- 1-212-456-7890

For each telephone number identified in the text, the following information is extracted:

- the text identified
- area
- prefix of the number
- station value
- the type of the telephone (mobile/landline).

## How it works

The analyzer runs a short sequence of NLP++ passes:

- **kbinit** creates the `telephones` root concept in the knowledge base (KB).
- **Lines** segments the input into individual lines so numbers are matched one line at a time.
- **telephone** matches several phone-number shapes. Each rule variant uses `@PRE length()` tests to select a shape by its digit-group sizes (for example 3-3-4 for North America, 3-4-4 for UK, 1-3-5 for short national numbers), and its `@POST` extracts `area`, `prefix`, and `station`. A separate variant handles solid, unseparated digit runs (optionally prefixed with `+`) by slicing the digits out by position.
- **telKB** stores each matched number as a numbered `telephone` concept under `telephones` and copies its attributes onto that concept.
- **output** writes the collected KB to `telephones.kbb` and exports the numbers to `output.json`.

To run the analyzer, create a text file in the input folder consisting of the text to be parsed.
