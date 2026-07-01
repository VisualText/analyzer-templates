# Knowledge Base

A starter analyzer that builds, saves, and exports a knowledge base as JSON.

## Analyzer Notes

This template shows the minimal plumbing for working with an NLP++ knowledge base (KB). It is a good starting point when your analyzer needs to accumulate information into a KB and write it back out.

- **`kbinit`** creates a `kb` concept off the knowledge-base root and stores it in the global variable `G("kb")`, then populates a small example hierarchy (`animals` → `dog`, `cat` with `sound` and `legs` attributes). This is where you build your KB — either with literal concepts and attributes as shown, or from matches produced by your own grammar passes.
- **`output`** persists the KB with `SaveKB(...)` and exports a human-readable JSON view with `JsonKB(...)`. Both functions live in the shared `spec/KBFuncs.nlp` library that every template includes.

To run the analyzer, create a text file in the `input` folder (the sample text is not parsed — the KB is built in `kbinit`). After running, the knowledge base dump `kb.kbb` and `kb.json` appear in the analyzer's output log (e.g. `input/<file>.txt_log/`).
