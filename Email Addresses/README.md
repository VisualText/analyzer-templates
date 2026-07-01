# Email Addresses

An analyzer that finds email addresses in text and breaks each one into its parts.

## Analyzer Notes

This is an NLP++ analyzer that scans plain text, locates the email addresses it contains, and decomposes each one into its component fields. A wide variety of address shapes are recognized, including:

- Standard addresses, e.g. `john.doe@example.com`, `mary.smith123@gmail.com`
- Local names with `.`, `_`, `-`, or `+` tags, e.g. `sarah_j@example.org`, `jennifer.smith+work@emaildomain.net`, `support-team123@techsupport.net`
- Hyphenated and multi-label domains, e.g. `contact.us@my-website.org`, `user1234@subdomain.example.com`
- Country-coded top-level domains, e.g. `jane_doe@outlook.co.uk`, `alice.smith@dept.departmentname.university.edu.uk`
- Spelled-out, anti-spam forms, e.g. `kenethfpp at mails dot yahoo dot uk` (the words `at` and `dot` stand in for `@` and `.`)

Sample addresses to try live in `input/text.txt`.

### Fields extracted

For each email address the analyzer pulls out and stores the following, then emits them as JSON:

- **local** — the local name, i.e. the text before the `@`, e.g. `john.doe`
- **domainname** / **dn** — the registered domain, e.g. `example`, `my-website`
- **tld** — the top-level domain, e.g. `com`, `org`, `net`
- **cd** / **country** — the country-code label and its resolved country name when the address uses a country-coded TLD, e.g. `uk`

Each address is collected under the `Emailaddrs` concept in the knowledge base and given a numeric `emailadd-id`.

## How it works

The analyzer runs a short sequence of NLP++ passes:

- **kbinit** creates the `Emailaddrs` root concept in the knowledge base (KB).
- **funcs** declares the helper functions used to extend, store, and JSON-serialize the matches.
- **Lines** segments the input into individual lines so addresses are matched one line at a time.
- **email1** is the core recognizer: several rule variants match `local@domain.tld` shapes (single-dot, multi-dot, and country-coded domains) as well as the spelled-out `at`/`dot` forms, and record the `local`, `domain`, `tld`, and `country` fields.
- **email11 / email12** attach a preceding local name to the spelled-out domain variants and normalize the result back into a single `_email` node.
- **email2–email6** gather any trailing `.label` domain segments (e.g. the `.uk` in `...university.edu.uk`) into the address, tidy up whitespace, and lift the resolved country onto the node.
- **email7** stores each finished address as a numbered `email` concept under `Emailaddrs` and copies its fields onto that concept.
- **output** serializes the collected KB to JSON.

## Output

After a run, the extracted addresses are written as JSON to the run's log folder, e.g. `input/text.txt_log/output.json`.

To run the analyzer, place a text file containing the text to be parsed in the `input` folder, then run the analyzer over it.
