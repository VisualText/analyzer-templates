# URLs

An analyzer that finds hyperlinks (URLs) in text and breaks each one into its parts.

## Analyzer Notes

This is an NLP++ analyzer that scans plain text, locates any hyperlinks it contains, and decomposes each link into its component fields. A wide variety of link shapes are recognized, including:

- Full schemed links, e.g. `https://en.wikipedia.org/wiki/Machine_learning`
- File-transfer links, e.g. `ftp://ftp.example.com/myfile.zip`
- Bare `www.` and sub-domain hosts, e.g. `www.wired.com`, `music.youtube.com`
- Links with query strings, e.g. `https://www.google.com/search?q=example`
- Multi-part top-level domains, e.g. `download.mozilla.org.uk`

Sample links to try live in `input/text.txt`.

### Fields extracted

For each hyperlink the analyzer pulls out and stores the following, then emits them as JSON:

- **scheme** — the protocol, e.g. `https` (Secure Hypertext Transfer Protocol), `http`, or `ftp` (File Transfer Protocol)
- **subdomain** — the host prefix, e.g. `en` (English), `www`, `music`
- **domain** — the registered name, e.g. `wikipedia`, `youtube`, `mozilla`
- **tld** — the top-level domain, e.g. `org`, `com`, `edu`
- **country** / **countryname** — the country-code TLD and its expansion when present, e.g. `uk`
- **pagepath** — the path (and any query string) after the host, e.g. `wiki/Machine_learning`

Each link is collected under the `Links` concept in the knowledge base and given a numeric `link-id`.

## Output

After a run, the extracted links are written as JSON to the run's log folder, e.g. `input/text.txt_log/output.json`.

## Running

To run the analyzer, place a text file containing the text to be parsed in the `input` folder, then run the analyzer over it.
