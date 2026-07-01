# Address Parser

A parser for American postal addresses

## Analyzer Notes

This is an NLP++ Analyzer that parses through text and identifies addresses (in USPS formats) listed anywhere in the text.

Some sample addresses can be found in `input/text.txt`.

Here are some examples:

- 123 Main Street, Cityville, 64775
- 4321 OAK ST, OAKTON MD 12345-6789
- 12 1ST ST NW, HAMPTON IA 50441-1902
- HC 72 BOX 293 A, DULUTH MN 55811-9702 (Highway Contract)
- RR 2 BOX 152 (Rural Route)
- PO BOX 293 (Post Office Box)

From each address, the following information is extracted (depending on the type of address, all or some of these fields are produced):

- House number
- Street number
- Street name
- Street suffix (the USPS abbreviation, like ST for Street)
- Street type (the spelled-out form, like Lane or Road)
- City
- State
- Pincode / ZIP code
- Country
- Type of address (individual, RuralRoute, HighwayContract, or post box)

Additionally, Rural Route and Highway Contract addresses are recognized, and for these the Rural Route / Highway Contract number and the Post Office box number are extracted.

All of this information is made available in JSON format. A sample output can be found (for the sample text) in `input/text.txt_log/output.json`.

To run the analyzer, create a text file in the input folder consisting of the text to be parsed.
