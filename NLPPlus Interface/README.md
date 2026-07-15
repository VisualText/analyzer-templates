# NLPPlus Interface

Imports JSON from the NLPPlus Python/NPM packages into the knowledge base and exports results back out as JSON.

A two-way data interface between the NLPPlus packages and an NLP++ analyzer: JSON handed in from a script is converted to a KBB and loaded into the knowledge base, then the knowledge base is exported back out as JSON for the script to read.

## Analyzer Notes

The [NLPPlus package for Python](https://github.com/VisualText/py-package-nlpengine) and the [NLPPlus package for NPM](https://github.com/VisualText/npm-package-nlpengine) let a script run one of your analyzers and exchange structured data with it. This template shows both directions of that exchange:

- **Import** — a script hands JSON to the analyzer; the analyzer loads it into its knowledge base (KB).
- **Export** — the analyzer writes its results as JSON; the script reads them back.

Neither side needs an LLM or any statistical model. The JSON ⇄ KB conversion is deterministic and human-readable.

### Import: JSON → KBB → knowledge base

1. A script places a `<name>.json` file in the analyzer's `kb/user/` folder. From Python (the NPM API mirrors it):

   ```python
   import NLPPlus
   # from a Python object...
   NLPPlus.put_json_object("NLPPlus Interface", {"data": {"source": "NLPPlus"}}, "data")
   # ...or from an existing JSON file
   NLPPlus.put_json_file("NLPPlus Interface", "data/mydata.json", "data")
   ```

2. On the next run the **`json2kbb`** python pass (in `spec/`) converts every `<name>.json` that does not yet have a matching `<name>.kbb` into a `<name>.kbb` knowledge-base file. This pass **must run before the tokenizer** — it is the first line of `spec/analyzer.seq`. The engine then loads the `.kbb` into the KB like any other KB file.

3. **`kbinit`** fetches the imported concept off the KB root (for the bundled `kb/user/data.json`, whose single top-level key is `data`, that concept is named `data`) and holds it in a global so later passes can read it.

To rebuild after editing a `.json`, delete its `.kbb` and run again — an existing `.kbb` is left untouched so hand-edited KBs are never clobbered.

### Export: knowledge base → JSON

**`output`** writes the KB back out with `JsonKB(...)` to **`output.json`**. That filename matters: the NLPPlus package reads it back for you as `results.output` (a parsed JSON object) and `results.output_json` (the raw string):

```python
results = NLPPlus.analyze("some text", "NLPPlus Interface")
data = results.output          # parsed JSON object built from output.json
raw  = results.output_json     # the same thing as a string
```

`output` also saves a human-readable `data.kbb` dump for debugging. Both `JsonKB` and `SaveKB` live in the shared `spec/KBFuncs.nlp` library that every template includes.

## Pass sequence (`spec/analyzer.seq`)

1. `json2kbb` — **import**: build `data.kbb` from any `data.json` in `kb/user/`.
2. `dicttokz` — tokenize the input text.
3. `KBFuncs` — shared knowledge-base function library.
4. `kbinit` — fetch the imported concept(s) into a global.
5. `output` — **export**: write `output.json` (and a `data.kbb` debug dump).

## Extending

This template deliberately just round-trips the data so you can see both ends of the interface working. In a real analyzer you would, between `kbinit` and `output`, add grammar passes that read the imported KB to drive the parse (look up values, tag matches in the text, grow new concepts) and then shape exactly what you hand back in `output.json`. See the other templates for how grammar passes add concepts and attributes to a knowledge base.

The results are written into the running input's log folder (e.g. `input/text.txt_log/output.json` and `data.kbb`).
